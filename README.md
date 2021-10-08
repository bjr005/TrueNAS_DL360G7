# TrueNAS_DL360G7

### TrueNAS SCALE patched for P410i in HBA-mode

###### Byggmiljö för TrueNAS Scale finns här: https://github.com/truenas/scale-build

    cd /build/
    git clone https://github.com/truenas/scale-build

###### Källkod för hpsahba finns här: https://github.com/im-0/hpsahba

    cd /build/
    git clone https://github.com/im-0/hpsahba

###### Ladda hem källkod för TrueNAS

    cd /build/scale-build/
    make checkout

###### Patcha kärnan

    cd /build/scale-build/sources/kernel
    patch -p1 < /build/hpsahba/kernel/version/*.patch

###### Patcha grub (aktivera den inpatchade funktionen)

    cd /build/scale-build    
    echo GRUB_CMDLINE_LINUX_DEFAULT=\"$GRUB_CMDLINE_LINUX_DEFAULT hpsa.hpsa_use_nvram_hba_flag=1\" >> sources/middlewared/src/freenas/etc/grub.d/11_bjorne_p410i_patch      

###### Bygg paket

    cd /build/scale-build/
    make packages

###### Bygg uppdateringsaket

    cd /build/scale-build/
    make update

###### Bygg ISO

    cd /build/scale-build/
    make iso
