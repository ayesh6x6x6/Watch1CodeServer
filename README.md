<h1>Steps to setup the server</h1>
<ul>
    <li>Download the zip file and extract it locally.</li>
    <li>Move the project to your <em>/home</em> directory.</li>
    <li>Switch to the project folder in command line and enter <strong>npm install</strong>.</li>
    <li>That should install the required dependencies of <em>mqtt, cassandra-driver, exceljs and pcap2csv</em> , otherwise manually install them.</li>
    <li>Open <strong>testAutomater.js</strong> file and change the <em>server_file</em> and <em>pcaps</em> constants to point to your exact <strong>server.js</strong> file as shown in the default value and also to your <strong>pcaps</strong> directory where the throughput.csv file will be saved.</li>
    <li>If running a Samsung watch, change the <em>targetWatch</em> constant here to the address of your watch too.</li>
    <li>Install Cassandra DB on your machine. Steps can be found at this link http://cassandra.apache.org/download/</li>
    <li> <p>After installation, an instance/node of cassandra should be running automatically, check status by running
        <strong>nodetool status</strong> or <strong>sudo service cassandra status</strong>. Both should give you an active or running status for one node. </p>  
        <p>Note: If you get nodetool error or service cassandra status returns that the service has exited, it means that cassandra is crashing, and probably has to do with the amount of space that is required. Try increasing your VM RAM to about 16 GB or so and retry.</p>   
    </li>
    <li>Additionally, you will need an MQTT broker running locally, try using PONTE npm broker. Installation and setup steps can be found at https://www.npmjs.com/package/ponte</li>
    <li>Once the environment is setup and the broker is running, start the server.</li>
    <li>Change the experiment number by modifying the <em>exp_num</em> variable if you run the experiment more than once. This will create a new record/table in the DB for every experiment you run.</li>
    <li>The server displays all the data it receives from the watch and also saves it in the DB with a unique key called <em>timestamp</em>.</li>
    <li>You can view the entries in the DB by running <strong>cqlsh</strong> on command line and entering the Cassandra Query Language(CQL) shell. From there just enter <strong>select * from watch_analytics.experiment#</strong> with your experiment # and view the results.</li>
    <li>Change the <em>tcconfigprofiles</em> variable to your downloaded project directory and <strong>tcconfigprofiles</strong> directory under it </li>
    <li>Change the <em>network_driver</em> variable to your wireless adapter name, when you run <em>ip addr</em> or <em>ifconfig</em>.</li>
    <li>Similarly change the <em>pcaps</em> variable to your pcaps directory location in your downloaded project.</li>
    <li>If running an Android wearable like Huawei Watch 3, 
        <ol>
            <li>Download the Nativescript Android App from https://github.com/ayesh6x6x6/Watch3-Android-NativescriptApp.</li>
            <li>Move the downloaded project to the same location as your Main Server (this project). </li>
            <li>Go to your watch and enable adb debugging under developer options.</li>
            <li>Also enable Wi-fi debugging or debugging over Wi-fi which will give you an address to connect to along with the port number, usually 5555 by default.</li>
            <li> change the <em>adb_huawei_addr</em> variable to the IP address of your watch with the port number as the default value shows.</li>
            <li>Lastly, install the Nativescript CLI globally by running <em>npm install -g nativescript</em>.</li>
        </ol>
    </li>
    <li>If running a Fitbit Device,
        <ol>
            <li>Download the Fitbit Device Fitbit App from https://github.com/ayesh6x6x6/Watch2FitbitApp</li>
            <li>Move the downloaded project to the same location as your Main Server (this project).</li>
            <li>Download the Fitbit App on your phone which is the primary pair of the Fitbit device.</li>
            <li>Enable bluetooth and Wifi on your phone and open the app.</li>
            <li>Select your device and enable <em>developer bridge</em> from the developer options.</li>
            <li>On your Fitbit device go to settings and enable the Developer Bridge too.</li>
            <li>When running the server and having a Fitbit device, a second shell will open as <strong>fitbit$</strong>, enter the command <em>install</em> here.</li>
        </ol>
    </li>
    <li>For network shaping part, you will need to install <strong>tcconfig</strong>. Follow these steps:- 
        <ol>
            <li>On debian/ubuntu enter <strong>wget https://github.com/thombashi/tcconfig/releases/download/v0.19.0/tcconfig_0.19.0_amd64.deb</strong> </li>
            <li>Follow by this command <strong>sudo dpkg -i tcconfig_0.19.0_amd64.deb</strong></li>
        </ol>
        You will also need to install Wireshark to use the tshark command line utility, this is simply done from the <em>Ubuntu Software</em>. 
    </li>
    <li>If you get the following error, <em>couldn't run /usr/bin/dumpcap in child process: Permission Denied</em> or something similar its a permissions related issue and add your user to the wireshark group by-
        <ol>
            <li>sudo dpkg-reconfigure wireshark-common</li>
            <li>choose answer as "YES" .Then add user to the group by</li>
            <li>sudo adduser $USER wireshark</li>
            <li>Restart your machine or wireshark.</li>
            <li>The pcaps you capture should not be locked, a useful link- https://askubuntu.com/questions/458762/how-to-enable-wireshark-without-running-as-root-in-trusty-14-04</li>
        </ol>
    </li>
    <li>After successfull run, in the <em>pcaps</em> directory, you should get a <strong>throughput.csv</strong> file which has the network 
    related information. For every re-run of the same experiment, remove the old pcaps and csv file. For new experiments, change <em>exp_num</em> and the <strong>Examples.xlsx</strong> file.</li>
    <li>Examples.xlsx has your episode and experiment information which will be automated, add new episodes with new network profiles and watch No. where 1 is Samsung, 2 is Fitbit, 3 is Huawei and 4 is Apple.</li>

</ul>