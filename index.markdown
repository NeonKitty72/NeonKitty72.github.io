---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
title: NeonKitty's VRChat Avatar Creation Docs
---

This are some helpful references I use for VRChat avatar editing and some of the more complex things I've learned. 

This assumes you have access to and use: 
- Blender
- Substance painter
- Unity 2022


## I want to Change the UV Map layout for an object (mesh) that already has a UV Layout
Create a new UV map, and bake the old UV onto the new UV. 
- [How to Bake Textures from One UV Map to Another in Blender (Tutorial)](https://www.youtube.com/watch?v=wsO1eozb1Qk)

TODO how to bake all UV's, not just color


## I want to Kitbash an avatar
There's multiple ways to do this. This is just how I did it - based around making a new base avatar mesh based on the other avatar's mesh's. 

### 1. Make a new base mesh in Blender with all the parts from other avatars
1. For each avatar, delete the parts of the mesh that you don't need. IE, if you only want the hair, delete the body + head. If you only want the tail, delete the body + hair + ears, etc.
1. Manually move all the objects to where you want them on the final avatar.
1. Merge the armatures
    1. Basically, every armature should have similar things. IE, two avatars will have arm and hand bones, tail bones, hair bones, etc. You'll pick one mesh as your base armature; On the other armature, delete any duplicate bones. But keep the bones that are unique to each armature. For instance, on a dress, you'd want to delete the arm and shoulder bones, since the base mesh will have those. But you'd want to keep any skirt bones, since the base mesh wouldn't have that.
    1. Merge the armatures.
    1. For the bones that are unique to each mesh, you need to link them together.
    1. [Tutorial on attaching clothes to your avatar that covers this well](https://www.youtube.com/watch?v=RlJ3NXjQp38)
1. Export the mesh - File > Export > FBX; In the popup, on the right hand side, make sure to change Apply Scalings to be "FBX Units Scale"


### 2. Setup the Avatar in Unity
Note: I got lucky on this part and was kitbashing an avatar from the same creator so most of these things lined up automatically, like animations. And I was only replacing hair and clothes, so the base body mesh was mostly the same. IDK all the bits of kitbashing from here if you're doing something more complex like swapping a head.

1. Drag and drop the FBX into your VRChat avatar Unity project
1. Drag and drop the kitbash model into your scene
1. Copy the copmonents from the base Avatar to your new avatar
    1. Import the base avatar's unity package into your unity project
    1. Drag and drop the base model into your scene
    1. Use Pumpkin's Avatar Tools to copy components from the base to the kitbash model
        1. Select your kitbash model in the scene
        1. In Pumpkin's avatar tools, click "select from scene" in the top and make sure it picks up your kitbash model
        1. Select the base avatar in the scene
        1. In Pumpkin's avatar tools, down in the Copy Components section, click Select from Scene. Make sure it picks your base model
        1. Unselect Skinned Mesh Rendered and Mesh Renderers
        1. Click Copy Selected
1. Now it's time to clean up the copied components.
    1. Rename the mesh on the new kitbash'd avatar to match the name of the base mesh from the base avatar
        1. All of the animations (blendshapes, etc) from the base avatar rely on the name of that base mesh, so if the body on the base mesh is named "Body.001", then your new kitbashed avatar needs to use "Body.001"
        1. If you're adding a new face on to an avatar body, you might just need to re-create the animations and animation layers. Sorry.
    1. In the VRChat SDK, in Builder, do the quick fixes for everything that's wrong. That will fix things like the models being read only.
    1. In the kitbash models' VRC Descriptor, set the mesh for visemes and anything else.
    1. Add an animator to your kitbash mesh
        1. Set the avatar to a new avatar 
            1. (TODO making an avatar)
        1. Check Apply Root Motion
        1. Set Culling Mode to Cull Update Transforms
1. Other things!
    1. For instance, I needed to change the physbones on my kitbash model's hair since it was new hair; so I looked at the physbone parameters on the avatar I stole the hair from, and copied the physbone properties over there. Since the kitbash model has the same hair bones, since we merged the armature in blender, it worked fine. Copying animations might even work, as long as the mesh names line up.
1. Upload the avatar!


