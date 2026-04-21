# Using Nordic's simulated Sensor Driver

- Add following lines in the file _nrf54l15dk_nrf54l15_cpuapp.overlay_. There is no need to delete existing content of this file!

      / {
         sensor_sim: sensor_sim{
               compatible = "nordic,sensor-sim";
               acc-signal = "wave";
               base-temperature = < 15 >;
               base-pressure = < 90 >;
         };
      };

- Replace in __main.c__ file the line <code>#define SENSOR_NODE DT_NODELABEL(lps22hb)</code> by the following one:

      #define SENSOR_NODE DT_NODELABEL(sensor_sim)
  
