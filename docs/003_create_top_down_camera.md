# Create top down camera w/ movement and rotation

1. Create a Node3D object.

    <img width="752" alt="Screenshot_2023-09-10_at_10_12_59_PM" src="https://github.com/zhifez/godot-notes/assets/33366655/502aa3f2-e8e3-4d99-8af7-cc781793b582">

2. While selecting the object, create a **SpringArm3D** object within it, and then a **Camera3D** object within that SpringArm.

    <img width="258" alt="Screenshot 2023-09-10 at 10 19 38 PM" src="https://github.com/zhifez/godot-notes/assets/33366655/b5488f30-a394-45ee-8203-989ece6aea83">

3. Select the **Camera3D** object, under **Inspector > Transform > Rotation**, set the **X-axis** to **-35**, so that the camera would look downwards.

    <img width="847" alt="Screenshot 2023-09-10 at 10 22 22 PM" src="https://github.com/zhifez/godot-notes/assets/33366655/7a125dc8-a918-440f-9a7d-586764459c73">

4. Next, select the **SpringArm3D** object, under **Inspector > Transform > Position**, set the **Y-axis** to **10**, so that the camera is positioned slightly higher off the ground.
  
5. Under **Inspector > Spring Length**, set the value to **10m**, this is to ensure the camera will always be 10m away from the pivot.

    <img width="269" alt="Screenshot 2023-09-10 at 10 41 01 PM" src="https://github.com/zhifez/godot-notes/assets/33366655/a8f0eafa-13be-4bb7-90fb-cf2ed537c6b1">


6. Populate the scene with a couple of cube meshes (MeshInstance3D) in front of the camera's facing direction, and run current scene. You should be able to see those meshes in the scene.

    <img width="374" alt="Screenshot 2023-09-10 at 10 31 21 PM" src="https://github.com/zhifez/godot-notes/assets/33366655/0b34e890-8b15-4769-9a98-76694dc09824">

7. To make it move, we need to add a script to link the movement to keyboard inputs. We can do so by selecting the **Node3D** object and click **"Attach a new... script"**.

    <img width="599" alt="Screenshot 2023-09-10 at 10 33 35 PM" src="https://github.com/zhifez/godot-notes/assets/33366655/7b92ab19-7b99-4dd9-bc22-405e4c125e07">

8. At the top of the script, we'll get a reference to the **SpringArm3D** and **Camera3D** so that we can handle them later.

    ```
    extends Node3D

    const SPEED = 10.0 # for setting the speed of the movement
    const INPUT_SENSITIVITY_X := 30.0 # for setting the rotational sensitivity on the x-axis
    const INPUT_SENSITIVITY_Y := 60.0 # for setting the rotational sensitivity on the y-axis
    
    @onready var spring_arm = $SpringArm3D
    @onready var camera = $SpringArm3D/Camera3D
    ```

9. To actually move the camera we'll update the `_process` function:

    ```
    var input_dir_move = Input.get_vector("ui_left", "ui_right", "ui_up", "ui_down")
    # retrieve the facing direction (forward) of the spring_arm
  	var direction = (spring_arm.transform.basis * Vector3(input_dir_move.x, 0, input_dir_move.y)).normalized()
  	position.x += direction.x * SPEED * delta
  	position.z += direction.z * SPEED * delta
    ```

10. Then, we'll rotate the Y-axis (left and right) of the top down camera, by rotating the **SpringArm3D** object.

    ```
    var input_dir_rotate = Input.get_vector("ui_left_2", "ui_right_2", "ui_up_2", "ui_down_2")
  	spring_arm.rotation_degrees.y -= input_dir_rotate.x * INPUT_SENSITIVITY_Y * delta
  	spring_arm.rotation_degrees.y = wrapf(spring_arm.rotation_degrees.y, 0.0, 360.0) 
    ```

11. Finally, we'll rotate the X-axis (up and down) of the top down camera, by rotating the **Camera3D** object.

    ```
    camera.rotation_degrees.x -= input_dir_rotate.y * INPUT_SENSITIVITY_X * delta
    camera.rotation_degrees.x = clamp(camera.rotation_degrees.x, -50.0, 10.0)
    ```

12. When we run the current scene again, we should be able to control the top down camera's movement and rotation:

    ![godot](https://github.com/zhifez/godot-notes/assets/33366655/c44b3a0f-cb40-46d0-af6a-e3116690ce6f)
