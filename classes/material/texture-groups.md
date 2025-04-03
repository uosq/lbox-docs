---
description: You can use this page to find a texture group you want to modify
---

# Texture groups

Compare the texture group with the values

Example:

```lua
materials.Enumerate(function (material)
      local group = material:GetTextureGroupName()
      local name = material:GetName()
      if (sky and group == "SkyBox textures") or group == "World textures"
      or string.find(name, "concrete", 1, true) or string.find(name, "wood", 1, true) or string.find(name, "nature", 1, true)
      or string.find(name, "wall", 1, true) then
         material:ColorModulate(1, 0, 0)
         material:AlphaModulate(1)
         material:SetShaderParam("$color2", Vector3(1, 0, 0))
      end
end)
```

Not stuff in the official docs, had to find it on my own

| GROUP NAME                                     | VALUE                 |
| ---------------------------------------------- | --------------------- |
| TEXTURE\_GROUP\_LIGHTMAP                       | Lightmaps             |
| TEXTURE\_GROUP\_WORLD                          | World textures        |
| TEXTURE\_GROUP\_MODEL                          | Model textures        |
| TEXTURE\_GROUP\_VGUI                           | VGUI textures         |
| TEXTURE\_GROUP\_PARTICLE                       | Particle textures     |
| TEXTURE\_GROUP\_DECAL                          | Decal textures        |
| TEXTURE\_GROUP\_SKYBOX                         | SkyBox textures       |
| TEXTURE\_GROUP\_CLIENT\_EFFECTS                | ClientEffect textures |
| TEXTURE\_GROUP\_OTHER                          | Other textures        |
| TEXTURE\_GROUP\_PRECACHED                      | Precached             |
| TEXTURE\_GROUP\_CUBE\_MAP                      | CubeMap textures      |
| TEXTURE\_GROUP\_RENDER\_TARGET                 | RenderTargets         |
| TEXTURE\_GROUP\_RUNTIME\_COMPOSITE             | Runtime Composite     |
| TEXTURE\_GROUP\_UNACCOUNTED                    | Unaccounted textures  |
| TEXTURE\_GROUP\_STATIC\_INDEX\_BUFFER          | Static Indices        |
| TEXTURE\_GROUP\_STATIC\_VERTEX\_BUFFER\_DISP   | Displacement Verts    |
| TEXTURE\_GROUP\_STATIC\_VERTEX\_BUFFER\_COLOR  | Lighting Verts        |
| TEXTURE\_GROUP\_STATIC\_VERTEX\_BUFFER\_WORLD  | World Verts           |
| TEXTURE\_GROUP\_STATIC\_VERTEX\_BUFFER\_MODELS | Model Verts           |
| TEXTURE\_GROUP\_STATIC\_VERTEX\_BUFFER\_OTHER  | Other Verts           |
| TEXTURE\_GROUP\_DYNAMIC\_INDEX\_BUFFER         | Dynamic Indices       |
| TEXTURE\_GROUP\_DYNAMIC\_VERTEX\_BUFFER        | Dynamic Verts         |
| TEXTURE\_GROUP\_DEPTH\_BUFFER                  | DepthBuffer           |
| TEXTURE\_GROUP\_VIEW\_MODEL                    | ViewModel             |
| TEXTURE\_GROUP\_PIXEL\_SHADERS                 | Pixel Shaders         |
| TEXTURE\_GROUP\_VERTEX\_SHADERS                | Vertex Shaders        |
| TEXTURE\_GROUP\_RENDER\_TARGET\_SURFACE        | RenderTarget Surfaces |
| TEXTURE\_GROUP\_MORPH\_TARGETS                 | Morph Targets         |
