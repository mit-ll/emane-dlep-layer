# EMANE DLEP Integration


## Building:
Make sure you've built and installed [LL-DLEP](https://github.com/mit-ll/LL-DLEP) first .

```bash
sudo apt-get install autotools-dev autoconf libtool uuid-dev libace-dev
./bootstrap && ./configure
make
sudo make install
```

## Running:
- Take a copy of `emanedleplayer.xml` and configure it's entries to match a config file from an LL-DLEP router (or the Dlep sample program defined in that project). E.g modify the multicast address and port, and set the interface to something both can see.
- Add this to an emane nem xml as a shim, e.g.:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE nem SYSTEM "file:///usr/share/emane/dtd/nem.dtd">
<nem>
  <transport definition="transvirtual.xml"/>
  <mac definition="rfpipemac.xml"/>
  <phy>
    <param name="fixedantennagain"         value="0.0"/>
    <param name="fixedantennagainenable"   value="on"/>
    <param name="bandwidth"                value="1M"/>
    <param name="noisemode"                value="outofband"/>
    <param name="propagationmodel"         value="precomputed"/>
    <param name="systemnoisefigure"        value="4.0"/>
    <param name="subid"                    value="2"/>
    <param name="txpower"                  value="0.0"/>
  </phy>
  <shim definition="emanedleplayer.xml"/>
</nem>
```
- spin up emane
- Use something like the Dlep tool to act as a peer: `Dlep config-file router.xml`

