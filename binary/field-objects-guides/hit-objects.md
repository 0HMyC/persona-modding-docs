---
title: Adding Hit Objects
layout: page
parent: 2D Field Objects
grand_parent: Binary Files
nav_order: 1
games: ['P3P']
---
<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

This will have info on adding custom Hit Objects to 2D Fields in P3P.

This guide will modify the Iwatodai Dormitory longue field to add a custom Hit Object, as it is a simple and convient field to test our edits with.

## Extracting Required Files

To begin, we will need to locate the abin file for the field we want to modify; in our case, we're looking for "b07_02.abin".

This can be located at the following paths:

* `field2d/p07_02.bin`, contained within at `bg/b07_02.abin`
* `field2d/bg/b07_02.abin`

Once you have located/extracted the abin file, we will now open it in Amicitia.

{: .todo }
> Add pictures so people can see what you're doing!!
>
> Make note of the languages!! You need to extract from the english CPK for this guide!

Expand the file list by double clicking on the "b07_02.abin" in Amicitia. We can now see all the files contained within the Dorm's field.

The files we'll need to extract to add custom Hit Objects are as follows:

* `h07_02_pck.dat`
* `h07_02.dat`
* `h07_02_name.dat`

Right click on the files in Amicitia, and click on the "Export" option. This will open up a window asking you where you want to save the file. You can export them wherever you want, though it is best to export them to the same folder that can be accessed quickly and conviently.

With all the files we will need extracted, we're ready to begin making our modifications to add custom Field Objects.

## Creating Hit Objects

### Naming our Object

To begin, we'll want to add a name to `h07_02_name.dat`, so that when we add a new object to the field, it will have a name displayed when we hover over it. Additionally, this is the easiest part of the process of adding a custom Hit Object, so it makes sense to start with that.

Open `h07_02_name.dat` in HxD, and you will the bytes of the file with decoded text over to the right. There are two changes we'll need to make here: incrementing the total number of names contained within the file, and adding a new name into the file.

![]({%link assets/images/binary/field-objects-guides/h07_02_name.png %})

To increase the total number of names contained within the file, we'll want to select 4 bytes from the offset `0x04` as shown in the below image. Then, click on the textbox next to `UInt32` in the Data inspector sidebar, and enter a higher number. Since we're only adding one name, we'll enter in 8.

![]({%link assets/images/binary/field-objects-guides/h07_02_name_edit_count.png %})

We've now specified that 8 Hit Object names are contained within the file, which will allow the game to load the new name we will add. Your view in HxD should now look like the image below.

![]({%link assets/images/binary/field-objects-guides/h07_02_name_edited_count.png %})

Next, we'll want to copy-and-paste an existing "block" of text in the file, so that we can be assured that the file remains formatted correctly. To do so, select `0x40 bytes` from offset `0x188`, and press Ctrl+C to copy the data.

![]({%link assets/images/binary/field-objects-guides/h07_02_name_copysel.png %})

Go to offset `0x1C8`, and paste (Ctrl+V) the bytes we copied. You should now have a duplicated block of text in the file, as seen below.

![]({%link assets/images/binary/field-objects-guides/h07_02_name_copied.png %})

Click at the start of the first `Sign-In Sheet` block, above the duplicate. Make sure you click inside the "Decoded text" section on the right, as this will allow us to normally type in the text we want to add.

![]({%link assets/images/binary/field-objects-guides/h07_02_name_copied_clickherebad.png %})

From here, simply write what you want the name of your object to be. For this guide, We'll type in `Hit Object Guide`.

![]({%link assets/images/binary/field-objects-guides/h07_02_name_finished.png %})

{: .warning}
> Make sure you are saving your files by navigating to File -> Save As; this ensures you'll keep the original files unmodified, allowing you to more easily go back and start over if you make a mistake.

Save the changes to a new file in a seperate location (see above warning), and we have successfully added a new name for our custom Hit Object to use.

### Defining our Object

Now, we're going to define what BF procedure and ID our Object should have in-game. To start, open `h07_02_pck.dat` in HxD. Next, select `0x4` bytes from offset `0x4`, and using the data inspector, edit the value from 7 to 8.

![]({%link assets/images/binary/field-objects-guides/h07_02_pck.png %})

![]({%link assets/images/binary/field-objects-guides/h07_02_pck_editcnt.png %})

Select `0x10` bytes from offset `0x58` as shown below, and copy the selected bytes. Then, paste them directly after the selected bytes. Your view should now look like the second image.

![]({%link assets/images/binary/field-objects-guides/h07_02_pck_copysel.png %})

![]({%link assets/images/binary/field-objects-guides/h07_02_pck_copied.png %})

Next, edit the bytes underlined below so that the values are `06` and `18` respectively. What we're doing here is telling the game that our object has the ID of 6, and that it should call procedure `0x18` (24 in decimal) from the `h07_02.bf` file when interacted with.

![]({%link assets/images/binary/field-objects-guides/h07_02_pck_finished.png %})

Save the file, and we have now defined the Script Procedure and ID of our object.

### Placing our Object

Finally, we are going to specify the position of our custom object in the field. For this guide, we will set our object at the coordinates X:200 Y:200, as a means of both ensuring we can set positions and that we won't possibly place our object right on top of another one accidentally.



{: .info}
> If you don't know how to replace files using Persona Essentials, see [the "Replacing Files" page.](/persona-modding-docs/getting-started/replacing-files)
