## Debian

You can upload a standard ISO file maually or use the **Download from URL** feature directly within your local Proxmox VE storage.
 
> **NOTE:** The **Download from URL** option for cloud-init images is effectively limited to Linux distributions due to Microsoft licensing restrictions.

Download from URL example

    https://cdimage.debian.org/cdimage/cloud/bookworm/latest/debian-12-generic-amd64.qcow2


## Windows
### VM config
Becuase Proxmox is built on Linux(KVM/QEMU), it doesn't support Window natively out of the box. You must download and upload **virtio-win ISO** to your Proxmox local storage. These drivers act as a bridge between Windows and Proxmox, without them, Windows will not be able to detect the virtual hard drive udring installation.

    https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/archive-virtio/virtio-win-0.1.285-1/

<img width="854" height="639" alt="image" style="width: 50%; height: auto;" src="https://github.com/user-attachments/assets/c5ef4772-4c1a-4ab4-862f-a430bc53be06" />

Select the corresponding OS type, add the Windows VirtIO ISO as a second CD/DVD drive, and leave the remaining configurations at their default settings.


<br/>

### Window Setup
During the Windows Setup process, the hard drive will not appear initially. This occurs because the installer lacks the native drivers required to communicate with Proxmox's SCSI controller.

<img width="638" height="480" alt="image" style="width: 50%; height: auto;" src="https://github.com/user-attachments/assets/efaf573e-e1f1-4d7e-9c03-c8ebf92a7897" />

<img width="639" height="475" alt="image" style="width: 50%; height: auto;" src="https://github.com/user-attachments/assets/b74f4646-e32e-43e2-8d31-ec468a9fbb2c" />

<img width="645" height="484" alt="image" style="width: 50%; height: auto;" src="https://github.com/user-attachments/assets/eab3ea04-ee6d-4d52-8aff-11f91ac6d9ac" />

Click Load Driver, browse to the VirtIO secondary drive, and select the correct folder for your operating system. For Windows 10, select the `w10\vioscsi.inf` driver.
<br>


### Install Guest Tools
Once the Windows installation is complete, run the VirtIO guest tools installer. This installs the remaining drivers and services, which fix and optimize:
- Graphics and Display
- Network
- Optimizes the virtual hard drive performance
- Memory Ballooning

<img width="777" height="589" alt="image" style="width: 50%; height: auto;"  src="https://github.com/user-attachments/assets/25ddc277-a216-4cd8-946a-1932f1a83b97" />

<img width="780" height="593" alt="image" style="width: 50%; height: auto;"  src="https://github.com/user-attachments/assets/d84a0e8f-6b32-48b4-8a7d-f49df6f8fe53" />

