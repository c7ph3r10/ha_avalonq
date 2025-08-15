# ha_avalonq
This repository is a simple template definition to create entities for the Canaan Avalon Q Home Miner to monitor and control the device.

# What it does
The avalonq.yaml file creates the following (helper) entities for your Canaan Avalon Q Home Miner device:

shell_commands:
set_<DEVICE NAME>_workmode:        SETTING THE WORKMODE WILL BE ADDED. HAVE TO ADJUST IT TO WORK with OTHER ENVIRONMENTS THAN MINE. UNTIL THEN YOU WILL NEED AN ADDITIONAL HELPER ENTITY
                                   MANUALLY CREATED WITH OPTION "Eco", "Standard", "Super". I USED input_select.<DEVICE NAME>. I WILL UPDATE THE REPOSITORY SOON FOR THIS.
set_<DEVICE NAME>_softon           Wake up the device from standby mode. It will return to its latest workmode automatically
set_<DEVICE NAME>_softoff          Activate standby mode
set_<DEVICE NAME>_lcdon            Turn on the LCD screen of the device
set_<DEVICE NAME>_lcdoff           Turn off the LCD screen of the device
set_<DEVICE NAME>_reboot           Reboot the device

command_line:
<DEVICE NAME>.Available            binary sensor to show whether the devices api is online/offline. Scan interval 5 seconds.
<DEVICE NAME>.api.stats            JSON "stats" response from the CGMiner API stored to the entities attributes. State of the entity is either OK or Error. Scan interval 30 seconds.
<DEVICE NAME>.api.litestats        JSON "litestats" response from the CGMiner API stored to the entities attributes. State of the entity is either OK or Error. Scan interval 15 seconds.
<DEVICE NAME>.api.coin             JSON "coin" response from the CGMiner API stored to the entities attributes. State of the entity is either OK or Error. Scan interval 30 seconds.
<DEVICE NAME>.api.summary          JSON "summary" response from the CGMiner API stored to the entities attributes. State of the entity is either OK or Error. Scan interval 30 seconds.
<DEVICE NAME>.api.pools            JSON "pools" response from the CGMiner API stored to the entities attributes. State of the entity is either OK or Error. Scan interval 30 seconds.
<DEVICE NAME>.api.devs             JSON "devs" response from the CGMiner API stored to the entities attributes. State of the entity is either OK or Error. Scan interval 30 seconds.
<DEVICE NAME>.api.devdetails       JSON "devdetails" response from the CGMiner API stored to the entities attributes. State of the entity is either OK or Error. Scan interval 30 seconds.
<DEVICE NAME>.api.version          JSON "version" response from the CGMiner API stored to the entities attributes. State of the entity is either OK or Error. Scan interval 30 seconds.
<DEVICE NAME>.api.config           JSON "config" response from the CGMiner API stored to the entities attributes. State of the entity is either OK or Error. Scan interval 30 seconds.

template entities:
<DEVICE NAME>.LcdOnOff.Switch      (switch) Turn on/off the miners LCD display
<DEVICE NAME>.LcdOnOff.Status      (binary sensor) Actual status of the LCD display. Used as "state" for <DEVICE NAME>.LcdOnOff.Switch
<DEVICE NAME>.Pool_Status          (binary sensor) Actual conectivity state to the mining pool
<DEVICE NAME>.Systemstatus         (sensor) Actual system status as a text
<DEVICE NAME>.State                (sensor) Actual system status as a number
<DEVICE NAME>.Uptime               (sensor) Uptime since last start in format x hour y minutes
<DEVICE NAME>.CPU_Model            (sensor) Miners CPU model
<DEVICE NAME>.ASIC_Model           (sensor) Mners ASIC model
<DEVICE NAME>.CPU_Freq             (sensor) Miners CPU frequency
<DEVICE NAME>.ID                   (sensor) Manufactureres unique id of the device
<DEVICE NAME>.Mode_Power_Output    (sensor) Setpoint power output for the current workmode (Eco = 800W, Standard = 1300W, Super = 1600W)
<DEVICE NAME>.ITemp                (sensor) Temperature inside the miners chassis
<DEVICE NAME>.HBITemp              (sensor) Inlet temperature of the hashboard
<DEVICE NAME>.HBOTemp              (sensor) Outlet temperature of the hashboard
<DEVICE NAME>.TMax                 (sensor) Max temperature of the 160 ASIC Chips. Each chip has a temperature. This is the max value overall.
<DEVICE NAME>.TAvg                 (sensor) Average temperature of the 160 ASIC Chips. Each chip has a temperature. This is the average value overall.
<DEVICE NAME>.TarT                 (sensor) Target temperature for the miners cooling algorithm
<DEVICE NAME>.Fan1                 (sensor) rpm of fan 1 (most probably first fan of the two inlet fans)
<DEVICE NAME>.Fan2                 (sensor) rpm of fan 2 (most probably second fan of the two inlet fans)
<DEVICE NAME>.Fan3                 (sensor) rpm of fan 3 (most probably first fan of the two outlet fans)
<DEVICE NAME>.Fan4                 (sensor) rpm of fan 4 (most probably second fan of the two outlet fans)
<DEVICE NAME>.FanR                 (sensor) Relative fan speed overall in percent. 
<DEVICE NAME>.Filter               (sensor) Overall runtime of the filter in minutes
<DEVICE NAME>.Network_Errors       (sensor) Total number of network errors since startup
<DEVICE NAME>.THSspd               (sensor) Currnt hashrate in TH/s
<DEVICE NAME>.Total_ASICs          (sensor) Total number of ASICS on the hashboard
<DEVICE NAME>.Cur_Load             (sensor) Current load in Watts
<DEVICE NAME>.FanErr               (sensor) Indicates whether a fan error exists
<DEVICE NAME>.Energy_per_TH        (sensor) Actual efficiendy in J/TH
<DEVICE NAME>.Ping                 (sensor) Latency (ms) to the current pool connected
<DEVICE NAME>.Worklevel            (sensor) Current worklevel (NOT WORKMODE). Seems not to be used. Always 0. Just kept it for research reasons
<DEVICE NAME>.Workmode.Status      (sensor) Actual workmode of the miner (0 = Eco, 1 = Standard, 2 = Super)
<DEVICE NAME>.Network_Difficulty   (sensor) Actual blockchain network difficulty
<DEVICE NAME>.Found_Blocks         (sensor) Miners found blocks
<DEVICE NAME>.Hardware_Errors      (sensor) Total number of hardware erorrs since startup
<DEVICE NAME>.Avg_Shares_per_Min   (sensor) Average number of shares per minute
<DEVICE NAME>.Hardware_ErrorsR     (sensor) Ratio of hardware errors to total number of shares
<DEVICE NAME>.Pool                 (sensor) URL of the connected pool
<DEVICE NAME>.Accepted_Shares      (sensor) Nubmer of accepted shares since startup
<DEVICE NAME>.Rejected_Shares      (sensor) Number of rejected shares since startup
<DEVICE NAME>.Rejection_Rate       (sensor) Rejection rate of the pool
<DEVICE NAME>.Latest_Share         (sensor) Time elapsed since latest share accepted
<DEVICE NAME>.Stratum_Difficulty   (sensor) Stratum difficulty
<DEVICE NAME>.CGMiner_Version      (sensor) CGMiner software version runing on the miner
<DEVICE NAME>.API_Version.Status   (sensor) API version running on the miner
<DEVICE NAME>.Firmware             (sensor) Firmware version running on the miner
<DEVICE NAME>.MAC_Address          (sensor) MAC address of the miners ethernet interface


# How to install
- Step 1: Create a folder named "packages" within the same directory where your configuration.yaml lives
- Step 2: Add the following linges to your configuration.yaml
homeassistant:
packages: !include_dir_merge_named packages/
- Step 3: Create a copy of the avalonq.yaml from this repository and copy it to the packages folder created before.
- Step 4: Do the following search/replace within the avalonq.yaml to adjust it to your environment

Replace \<IP-ADDRESS\> with the ip-address of your avalon q home miner
Replace \<DEVICE NAME\> with the name the miner template entites shall us as prefix. Keep it short an simple. No blanks.

- Step 5: Restart home assistant and check for the Avalon Q Miner entities. They should be shown under helper entities within ha.

If you have more than one Canaan Avalon Q Home Miner you will need a seperate avalonq.yaml per device. Make sure the above mentioned device name and of course also the file name are unique.
