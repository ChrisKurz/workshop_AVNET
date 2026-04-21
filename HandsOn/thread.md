# Using a Thread for LPS22HB sensor handling

1) Let's do the copmlete sensor handling within a Thread. Following parts should be covered wtihin the Thread function:
   - Initialization of the sensor driver
   - an entire loop, which handles sensor triggering, getting result, output of temperature and pressure, and to make a delay before the next measurement begins.

  So the Thread function should look like this:

    static void process_sample(void)
    {
        struct sensor_value pressure, temp;

        #define SENSOR_NODE DT_NODELABEL(lps22hb)
        const struct device *const dev = DEVICE_DT_GET(SENSOR_NODE);
        if (!device_is_ready(dev)) {
            printk("Sensor is not ready %s\n", dev->name);
    //      return 0;
        }
        printk("Sensor is ready!\n");

        while (1){
            // Fetch a sample from the sensor and store it in an internal driver buffer
            if (sensor_sample_fetch(dev) < 0) {
                printk("Error: Sensor sample update error\n");
    //          return;
            }

            // Get a reading from a sensor device (read pressure)
            if (sensor_channel_get(dev, SENSOR_CHAN_PRESS, &pressure) < 0) {
                printk("Error: Cannot read LPS22HB pressure channel\n");
    //          return;
            }

            // Get a reading from a sensor device (read temperature)	
            if (sensor_channel_get(dev, SENSOR_CHAN_AMBIENT_TEMP, &temp) < 0) {
                printk("Error: Cannot read LPS22HB temperature channel\n");
    //          return;
            }

            /* display pressure */
            printk("pressure: %d.%d kPa, ", pressure.val1, pressure.val2);
            //printk("Pressure: %.1f kPa, ", sensor_value_to_double(&pressure));

            /* display temperature */
            printk("Temperature: %.1f C\n", sensor_value_to_double(&temp));

            k_sleep(K_MSEC(2000));
        }
    }


2) Now we have to spawn the thread:


       #define MY_STACK_SIZE   500
       #define MY_PRIORITY     5

       K_THREAD_DEFINE(my_tid,         // Name of the Thread
                       MY_STACK_SIZE,  // Stack size in bytes
                       process_sample, // Thread entry function
                       NULL,           // 1st entry point parameter
                       NULL,           // 2nd entry point parameter
                       NULL,           // 3rd entry point parameter
                       MY_PRIORITY,    // Thread priority
                       0,              // Thread options
                       0);             // Scheduling delay (in milliseconds), zero for no delay


3) So the main() function is doing nothing related to the LPS22HB sensor handling:

       int main(void)
       {
           printk("LPS22HB Demo using a Thread\n");

           return 0;
       }   
