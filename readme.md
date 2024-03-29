# Synergist
Basically, it's a newly made Archetype for City of heroes. It has:

- Assault Primaries: A mix of both ranged and melee attacks, similar to the Dominator.
 
  - The Synergist versions of Assault sets swap out two of their attacks for upgrade-style powers that grant a small subset of powers from their list to the player's pets.
 
- Support/Defense secondaries: A combination of armors that are modified to provide half their benefit as auras, and general support powers like a Defender, Controller, Corrupter or Mastermind might have.

  - The first power in the set is always the pet. This delays the other powers a Synergist gets, but the upside is obviously the benefit of having a strong pet. Usually, this is equivalent to the 3rd pet of a MM at even-level, but the pair of pets at -1 level may be substituted if appropriate.

  - **TODO**: Learn how to make new pets so we aren't as limited to Mastermind pets for the powersets.

  - **TODO**: Adding a T9 "Merge" power to each set. Will do this once we figure out exactly how to work that. Probably should look at Kheldian forms.
    - Current intended implementation is that it will be a toggle that shuts itself off after X amount of time, provides a big version of the type of mitigation the rest of the set offers, and grants a small set of temp powers that are revoked when the power ends.
    - These temp powers will be considerably stronger to offset that they can't be enhanced.
- Inherent: As of right now, it's Partnership, which provides a +ToHit and +DMG to both pet and master while they are withing bodyguarding distance

# SETUP:

To set this up on your own server, you need to be set up for binning as explained [in this handy page](https://corps.ouro-comdev.com/index.php?title=Server_Setup_for_Making_Bins). Then you need the following:
- I recommend you use the .exes included in the folder `Build Bins with these exes`, as the existing ones don't have the `IsPetClass` flag available for classes, and using any binaries other than the ones I've provided will probably crash. It's a version of master modified to incorporate the pet class flag.

  - Optionally, you can edit the class .def files to comment out the `IsPetClass` line in `C_PC_Duo.def` and `V_PC_Mastermind.def` and build with the old exes, but you won't have bodyguarding or inspiration sharing in this case.

- Copy the `serverdata` folder directly into your binning setup's root directory. Overwrite any files it asks you about. The only files it should be replacing are below. I recommend you back these up before you do this.

  - classes.def

  - Epic.powersets

  - Epic_Powers.categories

  - Inherent.powersets

  - Inherent_Inherent.powers

  - Mastermind_Pets.powers

  - Player_Mastermind_Pets.categories

  - Player_Villain_Pets.categories

  - Villain_Pets.powersets

  - V_PC_Mastermind.def

- Bin the files.

  - It will complain about "BAD TRANSLATION" errors. Ignore it. It's just because I used native strings instead of pstrings like a dirty nasty boy.

   - TODO: Learn how to do message stores

  - If you bin with Develop branch EXEs, you'll probably get problems with message stores. If you do, make sure to keep a copy of `clientmessages-en.bin` to replace the bad message store bin develop produces.

- Next, generate new templates with `mapserver.exe -productionmode -templates` using the exes in `build templates and Run with these exes`

- Finally, put the included data folder into your root installation. It includes the icons for the archetype, and without them you'll get some weirdness. If you want, you can pigg them up with the other textures.

- Once you've got the bins, you should be able to run as normal. I have a separate setup for testing, and so I pigg the bins up with pig.exe or piglet and run that way. You will want to run using the exes I've provided in order to use the pet features.

- If your client or server starts getting all cattywampus after this, it means something is all hinky in the attributes table in your database. If that's the case, you may need to delete cohdb from your database (dbserver will rebuild it.) If you have characters, I recommend backing them up.

# Current Powersets:
## Assault

- Dark Assault

- Earth Assault

- Electricity Assault

- Energy Assault

- Fiery Assault

- Icy Assault

- Martial Assault

- Psionic Assault

## Support

- Hellfire Aura: A combination of Fiery Aura and Thermal Radiation, with Demons as the pets.

- Natural Instinct: Combination of Regen and Natural Affinity. Has Dire Wolf as pet.

- Nether Force: Combination of Dark Armor and Dark Miasma with the Lich as the pet.

- Ninjitsu: Pretty much the Stalker Ninjitsu with the two Ninja as pets. Turns out it fits for a Synergist Support set pretty well out 
of the box.

- Robotics: A combination of Force Fields and Traps with the Assault Bot pet. If we want it to be more defensive, we could opt for the Protector bot instead.

- Streetwise: Willpower with a couple of Leadership-flavored powers. This one has the most new powers and is also the least-tested right now. Bruiser is the pet.

- Super Serum: A combination of Invulnerability and Poisons, with the Commando as a pet.

- Mental Projection: A combination of light controls in the vein of Mind Control, plus some abilities culled from Fortunata Teamwork and including a modified form of the Phantasm from Illusion control, the Doppleganger! This uses newly-developed doppleganger flags to create a look-alike of its master with illusion powers.

### TODO: More sets for support, realign them to resemble the Guardian's Composition sets on Rebirth. (They're already quite similar.)

- Atmospheric Composition with a pet like /COXG/'s Wind Control Vortex

- Energy Composition with a Force Construct

- Ice Composition with an Ice Elemental or Snowman

- Might modify Natural Instinct to more resemble Organic Composition/Bio Armor

- Stone Composition with a Golem

- ~Once Doppleganger pets are made more widely available, make a Twin set of some kind. If we alter Natural Instinct, this would likely become where Regen's powers get put for lack of a better place, alongside elements of Empathy.~ (see above)

# Useful tidbits

The powers are mostly straightforward ports from other sets, with the obvious changes of the armor sets splitting their effects in half, half on self+pets only, half on everyone in radius.

The inherent uses a bit of a funny workaround: It grants a temp power to your pets that grants you and it the bonus, with the power disappearing when they leave range. I've set stacking to replace, so they shouldn't be stacking up in the case of multiple pets.
