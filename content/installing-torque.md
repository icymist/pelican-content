Title: Install Torque on a single multi-core Linux deskop
Date: 2015-03-27 11:53
Category: How To
Tags: linux


These days, all desktops easily have at least 4 or more cores.
We can use Torque to continuously use all these for running jobs in a batch.

Here, we install Torque on a linux desktop, with eight cores.
The desktop will act both as the torque server and also as the compute node on which computations are carried out.

Let us assume that we are trying to install it on the desktop with the fully qualified domain: bluesky.breezy.day. It is running openSuSE 13.2.
So, the hostname would just be bluesky. Then, do the following.

1.  Install all torque related stuff (torque-sever, torque-client, torque-mom, etc.) from [here](https://software.opensuse.org/package/torque). They are listed as unstable.

1.  Check the hostname. In my case, for some reason, ```hostname -f``` was not giving the fully qualified domain name bluesky.breezy.day, but just the hostnmame bluesky.

        :::bash
        hostname
        bluesky
        hostname -f
        bluesky

1.  Make sure that /etc/hosts has a line which lists the ip address of whatever you get for hostname in 1.

        :::bash
        echo '135.96.55.18 bleusky' >> /etc/hosts

1.  Create a serverdb file

        :::bash
        pbs_server -t create

1.  Create a nodes file

        :::bash
        cat server_priv/nodes
        bluesky np=6   # np is the number of cores on the desktop that you want to use

1.  Since, we are using the server also as the compute node, modify mom_priv/config. It should be:

        :::bash
        cat mom_priv/config   
        $pbsserver bluesky   # hostname running pbs server
        $logevent 225        # bitmap of which events to log

1.  Open up the ports for Torque in openSuSE firewall.

1.  Enable pbs_server, pbs_mom and pbs_sched in Yast > System > Services in exactly the order listed.
    Enabling the pbs_server AFTER pbs_mom, will not result in the pbs_server starting properly.

1.  Finally create a queue in which to run the jobs.

        :::bash
        qmgr -c "set server scheduling=true"
        qmgr -c "create queue default queue_type=execution"
        qmgr -c "set queue default started=true"
        qmgr -c "set queue default enabled=true"
        qmgr -c "set queue default enabled=true"
        qmgr -c "set server default_queue=default"
