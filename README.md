# eos-scripts
Collection of EOS scripts


## eos_download.py

This script is for situations where your CVP server doesn't have internet access but you have a jump host which can access CVP and has internet connectivity. The script downloads the specified EOS image locally and then uploads to the CVP server and creates an image bundle with the image in. It needs as inputs a valid arista.com profile token, the IP address of your CVP server and the root password along with the image version (e.g. 4.22.3F) and the WebGUI username and password of the CVP server you'd like to upload it with. These can be hardcoded into the script by editing the 'default' values in the parser lines of code or passed as commmand line options.

The script can also simply be used as a quick way to download images from arista.com without having to login to the website with SSO, browse through to find the right image and download through a browser. For this use case only the API token and image version are used. For virtual EOS images, use the --virt option, specifying vEOS, vEOS-lab or cEOS. Otherwise the standard image for a hardware switch is downloaded.

This script can also be used on an Eve-NG server to add EOS images ready for use in a topology. Use the --virt option to specify vEOS or vEOS-lab and add '--eve True' at the end of the arguments. This will download the image, covert to a qcow2 format, move to a folder named based on the image ready to choose in the GUI and finally delete the downloaded image.

Run the script using the following: .\eos_download.py --api {API TOKEN} --ver {EOS VERSION} [--ver {TERMINATTR VERSION}] [--img {INT|64|2GB|2GB-INT|vEOS|vEOS-lab|vEOS64-lab|cEOS|cEOS64|source} --cvp {CVP IP ADDRESS} --rootpw {ROOT PASSWORD} --cvp_user {GUI CVP USERNAME} --cvp_passwd {GUI CVP PASSWORD} --eve]

Requires tqdm, paramiko, requests and scp modules installing
