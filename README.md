# eos-scripts
Collection of EOS scripts


## eos_download.py

This script is for situations where your CVP server doesn't have internet access but you have a jump host which can access CVP and has internet connectivity. The script downloads the specified EOS image locally and then uploads to the CVP server and creates an image bundle with the image in. It needs as inputs a valid arista.com profile token, the IP address of your CVP server and the root password along with the image version (e.g. 4.22.3F) and the WebGUI username and password of the CVP server you'd like to upload it with. These can be hardcoded into the script by editing the 'default' values in the parser lines of code or passed as commmand line options.

The script can also simply be used as a quick way to download images from arista.com without having to login to the website, browse through to find the right image and download through a browser. For this use case only the API token, image version and optional type of image option (for International, 64-bit, vEOS etc. images). CVP releases can also be downloaded by specifying the version of CVP with the --ver argument in the form cvp-2020.1.1 for example and then with the --img argument, whether the ova, kvm, rpm or upgrade variant is required. CVP applications like Remedy, IPAM and CloudBuilder can be downloaded with the --img arguments remedy, ipam or cloudbuilder respectively.

Finally this script can be installed on an Eve-NG server to download an image and then createthe qcow2 image in a folder based on the image version for use in Eve topologies. Just add --eve to the command when run. If ZTP for the vEOS-lab image is not required, the --disable_ztpoption will mount the image and set ZTP to disabled. Note vEOS-lab images are best to use for Eve-NG.

If running the script on a non-shared environment, the user's API key could be hardcoded into the script to save having to use it on the command line. To do this, enter the API key as thedefault value in the argparse section and change the required value to False.

Run the script using the following: .\eos_download.py --api {API TOKEN} --ver {EOS VERSION|TERMINATTR VERSION|CVP VERSION} [--ver {EOS VERSION|TERMINATTR VERSION|CVP VERSION}] [--img {INT|64|2GB|2GB-INT|vEOS|vEOS-lab|vEOS64-lab|cEOS|cEOS64|source|ova|kvm|rpm|upgrade|ipam|remedy|cloudbuilder} --cvp {CVP IP ADDRESS}--rootpw {ROOT PASSWORD} --cvp_user {GUI CVP USERNAME} --cvp_passwd {GUI CVP PASSWORD} --eve --overwrite --disable_ztp] 

Requires tqdm, paramiko, requests and scp modules installing
