Download Link: https://assignmentchef.com/product/solved-ents749e-lab-7-ansible-ospf
<br>
This part is for individual work using a single router. Please use one of your assigned routers and note its IP address. In this part, you will write an Ansible playbook for remote RPC execution.

<ol>

 <li>On your VM, create a directory for your Ansible files (e.g. ~/ansible/).</li>

 <li>Create an inventory file for a single device (using the IP address of one of your routers) and save it in your Ansible directory. Define a symbolic alias name to refer to this device. Place this device in the “all” group.</li>

 <li>Create your ansible.cfg file and save it in your Ansible directory. You can copy its content from the slides. Make sure that the “inventory” directive refers to your inventory file.</li>

 <li>Create a playbook named sw_version.yaml with a single play that a) issues an RPC request that is equivalent to the “show version brief” operational-mode CLI command (note: you will need to pass a single input parameter to the RPC), and b) saves the output in a variable called “output” and displays it on the screen. Run your playbook and verify that the output is correct by comparing it against the output of the “show version brief” CLI command.</li>

 <li>Modify the playbook in such a way that it also saves the RPC response in a file called sw_version.json in JSON format in your Ansible directory. Display the content of the file on the screen and verify that the playbook works correctly.</li>

</ol>

Part II

For this part, work in groups of two (2 routers per student) and find out which router will be Router A,

Router B, Router C and Router D based on the received router assignments. In this part, you will write Ansible playbooks for router configuration and verification. You will need to create the same multi-area OSPF configuration as during the previous labs, but this time, using Ansible.

<ol>

 <li>Assume that you are given the address block 72.114.96.0/19. Your task is to set up a network consisting of 4 routers running OSPF as shown in the figure.</li>

 <li>Allocate IP addresses and networks from the address block and assign them to the routers’ interfaces. You will need to assign one network to each connected physical interface, and one network for each loopback interface. You can use the IP assignment from the previous labs to make things easier.</li>

 <li>Create one configuration template file (e.g. template.conf) that has the configuration information for both of your routers using a text editor. Use Jinja expressions and loops where necessary to make your template work with multiple routers and multiple interfaces and/or multiple OSPF areas in each router. The template should have the following components:

  <ul>

   <li>Interface configuration</li>

   <li>OSPF configuration (add the loopback interface as a passive interface)</li>

   <li>stateful firewall configuration.</li>

  </ul></li>

</ol>

You can reuse the configuration template file from the previous lab.

<ol start="4">

 <li>Modify the inventory file (or create a new one) such that a) it contains both or your routers, and b) it also contains the variables specific to each device in an appropriate hierarchy. Make sure that the hierarchy and names of your variables match those used in the configuration template.</li>

 <li>Write a playbook that loads and commits the configurations specified by the configuration template using the host variables defined in your inventory. Execute the playbook and verify that the correct configuration has been loaded and committed on both of your devices.</li>

 <li>Create a sub-directory called “ospf” is your Ansible directory.</li>

 <li>Write another playbook with two plays and multiple tasks that verify the configuration. The first play should send RPC requests to both of your devices and retrieve the content of the routes’ current routing tables. The content of each routing table should be saved in a separate file in the “ospf” subdirectory in text format, and the file name should be based on the router’s nickname (e.g. for router “srx50”, the file name could be “srx50_routes.txt”). The second playbook should loop over both of your devices and have each router ping the loopback interfaces of all remote routers. Set up the ping RPC in such a way that each remote interface is pinged three times. You may need to modify your inventory file and add more host variables for this task. The result of this play should be saved in separate files for each router in the “ospf” directory in JSON format, and the file name should be based on the router’s nickname (e.g. for router “srx50”, the file name could be “srx50_pings.json”).</li>

 <li>Check the content of the routing tables by viewing the routing table files and making sure that all remote loopback networks are present in all routers’ routing tables. Check the ping results by checking the content of the ping files and making sure that all pings were successful.</li>

</ol>