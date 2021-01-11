# NatPy

## Convert the units of particle physics quantities

---

### Packages needed:

- astropy
- numpy

---

### Basic Usage

Code levarages `astropy.units.core.Unit` and `astropy.units.quantity.Quantity` objects.

1. Run `import natpy`.
2. Access physical constants with symbol:

```
>>> natpy.const.c
<class 'astropy.constants.codata2018.CODATA2018'> name='Speed of light in vacuum' value=299792458.0 uncertainty=0.0 unit='m / s' reference='CODATA 2018'>


>>> natpy.const.hbar
<class 'astropy.constants.codata2018.CODATA2018'> name='Reduced Planck constant' value=1.0545718176461565e-34 uncertainty=0.0 unit='J s' reference='CODATA 2018'>
```

3. Specify base of natural units with `natpy.set_active_units()`. Pass a string corresponding to a list of default natural units, or a list of physical constants to set your own. List of default bases found in `natpy/default_values.py`.

4. Use `natpy.convert()` to convert between units, including necessary factors of natural units. Pass unit objects to obtain conversion factors. Pass quantity objects to perform conversions. E.g.

```
>>> import natpy as nat

# kg to keV
>>> nat.convert(nat.kg, nat.keV)
5.6173581670146864e+32

# Electron mass
>>> me = nat.convert(9.11e-31 * nat.kg, nat.keV)
>>> me
<Quantity 511.74132902 keV>

# Energy of electron with momentum of 1 MeV
>>> p = 1 * nat.MeV
>>> E = np.sqrt(p**2 + me**2)

# Convert to SI units
>>> nat.convert(E, nat.J)
<Quantity 1.79926309e-13 J>
```

5. `natpy.convert` may also be accessed a method for unit or quantity objects.

```
>>> import natpy as nat

>>>nat.GeV.convert(nat.fm**(-1))
5.067730716156395

>>>(3.0 * nat.m).convert(nat.s)
<Quantity 1.00069229e-08 s>
```

=======
Note: Summing quanties requires conventionally equivalent units.

6. See `tests/convert_test.py ` for more examples.
