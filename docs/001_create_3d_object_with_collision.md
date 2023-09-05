# Create 3D object with collision

The aim for this doc is to create a walkable floor for our player character.

1. To start with, click on the scene object and select the "+" add icon on the top left, which would open up the **Create New Node** menu.

    <img width="261" alt="Screenshot 2023-09-05 at 11 46 05 PM" src="https://github.com/zhifez/godot-notes/assets/33366655/1cc66cae-57e2-497f-971d-4f79661a6400">

2. Under the menu, double click on **StaticBody3D** to create it.

    <img width="726" alt="Screenshot 2023-09-05 at 11 46 48 PM" src="https://github.com/zhifez/godot-notes/assets/33366655/4cb472b9-dffa-4250-83dd-745e18b57707">

3. Select the **StaticBody3D**, and click on the "+" add icon again. This time, create both **MeshInstance3D** and **CollisionShape3D** within the GameObject.

    <img width="261" alt="Screenshot 2023-09-05 at 11 49 28 PM" src="https://github.com/zhifez/godot-notes/assets/33366655/bff8fb31-1a4d-42a7-b439-e081bd25fbd0">

4. Select the **CollisionShape3D**, under the **Inspector** tab, click on the **Shape: <empty>** field, and select **New BoxShape3D**.

    <img width="276" alt="Screenshot 2023-09-05 at 11 50 55 PM" src="https://github.com/zhifez/godot-notes/assets/33366655/3dfeea3a-1aed-4982-a5cd-76ba08d2b296">

5. This will create a collider for our GameObject, which can be seen on viewport:

    <img width="568" alt="Screenshot 2023-09-05 at 11 52 03 PM" src="https://github.com/zhifez/godot-notes/assets/33366655/c63d3240-b39c-4112-961a-27bec32d6a7f">

6. On the same **Inspector** tab, click on the newly created BoxShape, and there should be a sub-menu to edit its config.

    <img width="263" alt="Screenshot 2023-09-05 at 11 56 31 PM" src="https://github.com/zhifez/godot-notes/assets/33366655/54d1f9be-7d5b-4bcd-8dc6-db15d5143b12">

7. Change the **Y** value of **Size** to 0, and that should flatten the shape to a plane, that looks like this:

    <img width="581" alt="Screenshot 2023-09-05 at 11 57 20 PM" src="https://github.com/zhifez/godot-notes/assets/33366655/982d72e0-60f2-4103-aa16-9491a8bdaf76">

8. Next, we'll select the **MeshInstance3D** object, then on the **Inspector** tab, click on the **Mesh: <empty>** field and select **New PlaneMesh**. It should create a simple plane mesh:

    <img width="1044" alt="Screenshot 2023-09-05 at 11 59 47 PM" src="https://github.com/zhifez/godot-notes/assets/33366655/b9a44b3a-4d91-4b2f-93d4-d20c3f7ea715">

9. It's probably not that visible, but the size of the CollisionShape3D is actually smaller than the plane mesh. 
  We have three choices here:

    - A, we can either reduce the Size of the plane mesh to 1:

        <img width="252" alt="Screenshot 2023-09-06 at 12 01 32 AM" src="https://github.com/zhifez/godot-notes/assets/33366655/0e75dd16-cdc8-4d36-8c23-8b3c4b9ba15b">

    - B, we can set the Size of the collider to 2:

        <img width="274" alt="Screenshot 2023-09-06 at 12 02 57 AM" src="https://github.com/zhifez/godot-notes/assets/33366655/5c4fefd1-0fce-4bb8-a280-92d8fb1e548b">

    - C, we can set the Sizes for both A and B to 1, and change the **Scale** of the **StaticBody3D** if we want to make it bigger:

        <img width="262" alt="Screenshot 2023-09-06 at 12 05 45 AM" src="https://github.com/zhifez/godot-notes/assets/33366655/6e24abc5-961b-4575-931a-be5cbecb281c">
