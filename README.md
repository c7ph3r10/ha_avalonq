# ha_avalonq
This repository is a simple template definition to create entities for the Canaan Avalon Q Home Miner to monitor and control the device.<br>
Using those entities it is possible to build dashboards (example not included) e.g. like this:

**Condensed View:**<br>
<img width="1666" height="448" alt="grafik" src="https://github.com/user-attachments/assets/aba2b63d-e7e0-4f3e-8b0f-ce308cfd37e3" />

**Monitoring View:**<br>
<img width="1674" height="661" alt="grafik" src="https://github.com/user-attachments/assets/10d15b56-5e21-4f23-a22b-bcc1a648f6cd" />

**Details View:**<br>
<img width="1665" height="1920" alt="grafik" src="https://github.com/user-attachments/assets/ccd253bf-16c8-4469-9fa6-86fbe3d6f715" />


# What it does
The avalonq.yaml template definition file creates the following (helper) entities:

**Shell Commands:**<br>
<pre>
set_&ltDEVICE NAME&gt;_workmode:        SETTING THE WORKMODE WILL BE ADDED. HAVE TO ADJUST IT TO WORK with OTHER ENVIRONMENTS THAN MINE. UNTIL THEN YOU WILL NEED AN ADDITIONAL HELPER ENTITY MANUALLY CREATED WITH OPTION "Eco", "Standard", "Super". I USED input_select.<DEVICE NAME>. I WILL UPDATE THE REPOSITORY SOON FOR THIS.
set_&ltDEVICE NAME&gt;_softon           Wake up the device from standby mode. It will return to its latest workmode automatically
set_&ltDEVICE NAME&gt;_softoff          Activate standby mode
set_&ltDEVICE NAME&gt;_lcdon            Turn on the LCD screen of the device
set_&ltDEVICE NAME&gt;_lcdoff           Turn off the LCD screen of the device
set_&ltDEVICE NAME&gt;_reboot           Reboot the device
</pre>
  
**Command Line Entities:**<br>
<pre>
&ltDEVICE NAME&gt;.Available            binary sensor to show whether the devices api is online/offline. Scan interval 5 seconds.
&ltDEVICE NAME&gt;.api.stats            JSON "stats" response from the CGMiner API stored to the entities attributes. State of the entity is either OK or Error. Scan interval 30 seconds.
&ltDEVICE NAME&gt;.api.litestats        JSON "litestats" response from the CGMiner API stored to the entities attributes. State of the entity is either OK or Error. Scan interval 15 seconds.
&ltDEVICE NAME&gt;.api.coin             JSON "coin" response from the CGMiner API stored to the entities attributes. State of the entity is either OK or Error. Scan interval 30 seconds.
&ltDEVICE NAME&gt;.api.summary          JSON "summary" response from the CGMiner API stored to the entities attributes. State of the entity is either OK or Error. Scan interval 30 seconds.
&ltDEVICE NAME&gt;.api.pools            JSON "pools" response from the CGMiner API stored to the entities attributes. State of the entity is either OK or Error. Scan interval 30 seconds.
&ltDEVICE NAME&gt;.api.devs             JSON "devs" response from the CGMiner API stored to the entities attributes. State of the entity is either OK or Error. Scan interval 30 seconds.
&ltDEVICE NAME&gt;.api.devdetails       JSON "devdetails" response from the CGMiner API stored to the entities attributes. State of the entity is either OK or Error. Scan interval 30 seconds.
&ltDEVICE NAME&gt;.api.version          JSON "version" response from the CGMiner API stored to the entities attributes. State of the entity is either OK or Error. Scan interval 30 seconds.
&ltDEVICE NAME&gt;.api.config           JSON "config" response from the CGMiner API stored to the entities attributes. State of the entity is either OK or Error. Scan interval 30 seconds.
</pre>

**Template Entities:**<br>
<pre>
&ltDEVICE NAME&gt;.LcdOnOff.Switch      (switch) Turn on/off the miners LCD display
&ltDEVICE NAME&gt;.LcdOnOff.Status      (binary sensor) Actual status of the LCD display. Used as "state" for <DEVICE NAME>.LcdOnOff.Switch
&ltDEVICE NAME&gt;.Pool_Status          (binary sensor) Actual conectivity state to the mining pool
&ltDEVICE NAME&gt;.Systemstatus         (sensor) Actual system status as a text
&ltDEVICE NAME&gt;.State                (sensor) Actual system status as a number
&ltDEVICE NAME&gt;.Uptime               (sensor) Uptime since last start in format x hour y minutes
&ltDEVICE NAME&gt;.CPU_Model            (sensor) Miners CPU model
&ltDEVICE NAME&gt;.ASIC_Model           (sensor) Miners ASIC model
&ltDEVICE NAME&gt;.CPU_Freq             (sensor) Miners CPU frequency
&ltDEVICE NAME&gt;.ID                   (sensor) Manufacturers unique id of the device
&ltDEVICE NAME&gt;.Mode_Power_Output    (sensor) Setpoint power output for the current workmode (Eco = 800W, Standard = 1300W, Super = 1600W)
&ltDEVICE NAME&gt;.ITemp                (sensor) Temperature inside the miners chassis
&ltDEVICE NAME&gt;.HBITemp              (sensor) Inlet temperature of the hashboard
&ltDEVICE NAME&gt;.HBOTemp              (sensor) Outlet temperature of the hashboard
&ltDEVICE NAME&gt;.TMax                 (sensor) Max temperature of the 160 ASIC Chips. Each chip has a temperature. This is the max value overall.
&ltDEVICE NAME&gt;.TAvg                 (sensor) Average temperature of the 160 ASIC Chips. Each chip has a temperature. This is the average value overall.
&ltDEVICE NAME&gt;.TarT                 (sensor) Target temperature for the miners cooling algorithm
&ltDEVICE NAME&gt;.Fan1                 (sensor) rpm of fan 1 (most probably first fan of the two inlet fans)
&ltDEVICE NAME&gt;.Fan2                 (sensor) rpm of fan 2 (most probably second fan of the two inlet fans)
&ltDEVICE NAME&gt;.Fan3                 (sensor) rpm of fan 3 (most probably first fan of the two outlet fans)
&ltDEVICE NAME&gt;.Fan4                 (sensor) rpm of fan 4 (most probably second fan of the two outlet fans)
&ltDEVICE NAME&gt;.FanR                 (sensor) Relative fan speed overall in percent. 
&ltDEVICE NAME&gt;.Filter               (sensor) Overall runtime of the filter in minutes
&ltDEVICE NAME&gt;.Network_Errors       (sensor) Total number of network errors since startup
&ltDEVICE NAME&gt;.THSspd               (sensor) Currnt hashrate in TH/s
&ltDEVICE NAME&gt;.Total_ASICs          (sensor) Total number of ASICS on the hashboard
&ltDEVICE NAME&gt;.Cur_Load             (sensor) Current load in Watts
&ltDEVICE NAME&gt;.FanErr               (sensor) Indicates whether a fan error exists
&ltDEVICE NAME&gt;.Energy_per_TH        (sensor) Actual efficiendy in J/TH
&ltDEVICE NAME&gt;.Ping                 (sensor) Latency (ms) to the current pool connected
&ltDEVICE NAME&gt;.Worklevel            (sensor) Current worklevel (NOT WORKMODE). Seems not to be used. Always 0. Just kept it for research reasons
&ltDEVICE NAME&gt;.Workmode.Status      (sensor) Actual workmode of the miner (0 = Eco, 1 = Standard, 2 = Super)
&ltDEVICE NAME&gt;.Network_Difficulty   (sensor) Actual blockchain network difficulty
&ltDEVICE NAME&gt;.Found_Blocks         (sensor) Miners found blocks
&ltDEVICE NAME&gt;.Hardware_Errors      (sensor) Total number of hardware erorrs since startup
&ltDEVICE NAME&gt;.Avg_Shares_per_Min   (sensor) Average number of shares per minute
&ltDEVICE NAME&gt;.Hardware_ErrorsR     (sensor) Ratio of hardware errors to total number of shares
&ltDEVICE NAME&gt;.Pool                 (sensor) URL of the connected pool
&ltDEVICE NAME&gt;.Accepted_Shares      (sensor) Nubmer of accepted shares since startup
&ltDEVICE NAME&gt;.Rejected_Shares      (sensor) Number of rejected shares since startup
&ltDEVICE NAME&gt;.Rejection_Rate       (sensor) Rejection rate of the pool
&ltDEVICE NAME&gt;.Latest_Share         (sensor) Time elapsed since latest share accepted
&ltDEVICE NAME&gt;.Stratum_Difficulty   (sensor) Stratum difficulty
&ltDEVICE NAME&gt;.CGMiner_Version      (sensor) CGMiner software version runing on the miner
&ltDEVICE NAME&gt;.API_Version.Status   (sensor) API version running on the miner
&ltDEVICE NAME&gt;.Firmware             (sensor) Firmware version running on the miner
&ltDEVICE NAME&gt;.MAC_Address          (sensor) MAC address of the miners ethernet interface
</pre>

# How to install
- Step 1: Create a folder named "packages" within the same directory where your configuration.yaml lives
- Step 2: Add the following lines to your configuration.yaml<br>
<pre>
homeassistant:
  packages: !include_dir_merge_named packages
</pre>
- Step 3: Copy the avalonq.yaml from this repository to the packages folder.
- Step 4: Do the following search/replace within the avalonq.yaml to adjust it to your environment

Replace \<IP-ADDRESS\> with the ip-address of your avalon q home miner<br>
Replace \<DEVICE NAME\> with the name the miner template entites shall us as prefix. Keep it short and simple. No blanks.

- Step 5: Restart home assistant and check for the new entities. They should be shown under helper entities.

If you have more than one Canaan Avalon Q Home Miner you will need a copy of avalonq.yaml per device.<br>
Make sure the above mentioned device names and of course also the file names are unique.
