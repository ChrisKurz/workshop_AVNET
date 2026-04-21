# Using Workqueue for Sensor Handling

1) First, let's copy the _zephyr/samples/hello_world_ project to your own Workspace!

  > __IMPORTANT__: There is also a _nrf/samples/hello_world_ sample. Do __not__ use this one!!!

2) Click on _Add Build Configuration_ and use following settings:

   > __Board Target__:   nRF54L15DK/nRF54L15/cpuapp
   >
   > __Generate Only__:  ensure the check box is set
   >
   > Do not change the rest of the settings and click on _Generate and Build_ button.

3) Add following include instructions:

       #include <zephyr/kernel.h>
       #include <zephyr/drivers/sensor.h>

4) Let's handle the Sensor DeviceTree as a global variable. Add following lines just after the include instructions:

       #define SENSOR_NODE DT_NODELABEL(lps22hb)
       const struct device *const dev = DEVICE_DT_GET(SENSOR_NODE);

5) Let's define the workqueue variable <code>work</code>:

       struct k_work work;

6) The function we would like to call via a Workqueue Thread looks like this:

       static void process_sample(struct k_work *item)
       {
           struct sensor_value pressure, temp;

           // Fetch a sample from the sensor and store it in an internal driver buffer
           if (sensor_sample_fetch(dev) < 0) {
               printk("Error: Sensor sample update error\n");
               return;
           }

           // Get a reading from a sensor device (read pressure)
           if (sensor_channel_get(dev, SENSOR_CHAN_PRESS, &pressure) < 0) {
               printk("Error: Cannot read LPS22HB pressure channel\n");
               return;
           }

           // Get a reading from a sensor device (read temperature)	
           if (sensor_channel_get(dev, SENSOR_CHAN_AMBIENT_TEMP, &temp) < 0) {
               printk("Error: Cannot read LPS22HB temperature channel\n");
               return;
           }

           /* display pressure */
           printk("pressure: %d.%d kPa, ", pressure.val1, pressure.val2);
           //printk("Pressure: %.1f kPa, ", sensor_value_to_double(&pressure));

           /* display temperature */
           printk("Temperature: %.1f C\n", sensor_value_to_double(&temp));
       }

7) And finally, we modify the main function so it looks like this:

       int main(void)
       {
           printk("LPS22HB Demo - Workqueue\n");

           if (!device_is_ready(dev)) {
               printk("Sensor is not ready %s\n", dev->name);
               return 0;
           }
           printk("Sensor is ready!\n");

           k_work_init(&work, process_sample);

           while (true) {
               k_work_submit(&work);
               k_sleep(K_MSEC(2000));
           }
       }
