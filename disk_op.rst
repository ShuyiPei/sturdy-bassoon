:Author:
    overuns,
    Shuyi Pei
:Version: 1.0 of 2019/11/18

=======
disk op
=======

create disk
---

.. code-block:: bash

    qemu-img create -f raw a.img 512M

make fs
---

.. code-block:: bash

    losetup -Pf a.img
    losetup -l | grep a.img
    cfdisk /dev/loop1
    mkfs.ext4 /dev/loop1p1

unload disk
---

.. code-block:: bash

    losetup -d /dev/loop1

resize disk
---

.. code-block:: bash

    qemu-img resize -f raw a.img +512M

resize fs
---

.. code-block:: bash

    losetup -Pf a.img
    cfdisk /dev/loop1
    e2fsck -f /dev/loop1p1
    resize2fs /dev/loop1p1

[repeat unload disk]
---

use disk
---

.. code-block:: bash

    losetup -Pf a.img
    mkdir {a,b}
    mount /dev/loop1p1 a
    mount /dev/loop1p2 b
    umount {a,b}
    losetup -d /dev/loop1
    
