# pykumo
Python library to interact with Mitsubishi KumoCloud devices via their local API.

The hard work of generating the security token was done by https://github.com/sushilks/kumojs and that part is based heavily on his code, translated to Python by me.

## Interactive use
It's possible to use pykumo in an interactive shell to do debugging, investigation of possible new features, etc.

I recommend doing this work in a `virtualenv`, which web searching will describe if you're not familiar.

### Start an interactive Python shell
```
pip3 install pykumo
python3
```
### Set up KumoCloudAccount
Inside the Python shell:
```
import pykumo
account = pykumo.KumoCloudAccount.Factory()
```
This will prompt for your KumoCloud username & password
```
account.get_indoor_units()
```
If successful, `get_indoor_units` will print a list of your indoor units' serial numbers

### Get indoor units
```
kumos = account.make_pykumos()
unit = kumos['<indoor unit name>']
unit.update_status()
```
The indoor unit name is the human-readable name. If successful, `update_status` will print `True`. You can then make the various API calls on the `unit` object.

### Raw information from indoor unit
You can print the internal state of the indoor unit object, which includes the JSON information fetched from the unit itself. This is a good place to look when requesting support of additional pykumo features.
```
import pprint
pp = pp.PrettyPrinter()
pp.pprint(unit.__dict__)
```
