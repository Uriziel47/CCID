# Loading device

```c
		if (sscanf(getenv("TERMUX_USB_FD"), "%d", &fd) == 1)
		{
			libusb_device_handle *shandle;
			libusb_wrap_sys_device(ctx, (intptr_t) fd, &shandle);
			dev = libusb_get_device(shandle);
			DEBUG_COMM2("Termux FD: %s", getenv("TERMUX_USB_FD"));
		}
		if (dev != NULL)
		{
			DEBUG_COMM3("Termux FD: %s", getenv("TERMUX_USB_FD"), NULL);
```
# Yubico USB ids

see [https://support.yubico.com/hc/en-us/articles/360016614920-YubiKey-USB-ID-values]

VendorID: 0x1050
Yubico 5: 0x0407  

# Compiling

```bash
meson setup builddir -c_args=-D__TERMUX__
cd builddir
meson compile

meson install
cp ./libccid.so ~/../usr/lib/pcsc/drivers/ifd-ccid.bundle/Contents/Linux/libccid.so
```
