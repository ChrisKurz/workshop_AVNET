# Using a Thread for LPS22HB sensor handling

1) Let's do the copmlete sensor handling within a Thread. Following parts should be covered wtihin the Thread function:
   - Initialization of the sensor driver
   - an entire loop, which handles the sensor processing. We add a delay before next measurement is started. 

  So the Thread function should look like this - add it after the <code>process_sample()</code> function:

    static void sensor_thread(void)
    {
        struct sensor_value pressure, temp;

        #define SENSOR_NODE DT_NODELABEL(lps22hb)
        const struct device *const dev = DEVICE_DT_GET(SENSOR_NODE);
        if (!device_is_ready(dev)) {
            printk("Sensor is not ready %s\n", dev->name);
            while(1);
    //      return 0;
        }
        printk("Sensor is ready!\n");

        while (1){
            process_sample(dev);
            k_sleep(K_MSEC(2000));
        }
    }


2) Now we have to spawn the thread - add these lines after the <code>sensor_thread()</code> function:

       #define MY_STACK_SIZE   500
       #define MY_PRIORITY     5

       K_THREAD_DEFINE(my_tid,         // Name of the Thread
                       MY_STACK_SIZE,  // Stack size in bytes
                       sensor_thread,  // Thread entry function
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
