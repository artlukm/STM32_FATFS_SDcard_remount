<h1 align="center">Hi there
<img src="https://github.com/blackcater/blackcater/raw/main/images/Hi.gif" height="32"/></h1>
<h3 align="center">I present to your attention the bug FATFS of re-mounting the card.</h3>

If your code works fine, but after reinstalling the SD card, it no longer works, most likely you are facing the this problem.
When reinserting the card. Function f_mount() no longer works, returns an error FR_DISK_ERR.
to solve the problem, you need to add the function of zeroing the structure field in diskio.c.

void disk_DeInitialize (
	BYTE pdrv				/* Physical drive nmuber to identify the drive */
)
{
  disk.is_initialized[pdrv] = 0;
}

Add this function to f_mount, to call it when unmounting a disk.
See in the code STM32f4-discovery https://github.com/RomanYankov/STM32_FATFS_SDcard_remount.

Tutorial: SD card over SPI using STM32CubeIDE and FatFS
Reference :
https://01001000.xyz/2020-08-09-Tutorial-STM32CubeIDE-SD-card/
