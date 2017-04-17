Docker has the benefit of being a complete product (the **“batteries included”** model) but also providing **pluggability** in case you want to add things.

By default, Docker ships with a Overlay storage driver(In the older version, it ships with AUFS storage driver). However, other storage drivers are pluggable such as OverlayFS, Device Mapper, BTRFS, VFS, and ZFS. They all implement image composition and copy-on-write mechanism, among other features.

To see what storage driver your Docker engine is using, run:

`docker info`{{execute}}

Notice the Storage Driver: overlay line in this output. That means we’re using the stock OverlayFS driver.

Let’s look at the way Docker works with app generated data.
