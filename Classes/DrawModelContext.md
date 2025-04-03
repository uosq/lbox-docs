# DrawModelContext

Represents the context in which a model is being drawn in the DrawModel callback.

## Methods

> ### GetEntity ( )
>
> Returns the entity of the model (**can be nil**)
>
> nil entities might be dynamic props like the orange cone in **itemtest** that you can shoot, viewmodel weapon, resupply cabinet, etc
>
> Return type: **Entity**

---

> ### GetModelName ( )
>
> Returns the model's name
>
> Return type: **string**

---

> ### ForcedMaterialOverride ( mat: Material )
>
> Replace material used to draw the model. The material can be found or created by **[materials.Create / materials.Find](https://github.com/uosq/lbox-docs/blob/main/Libraries/materials.md)**
>
> Return type: nothing

---

> ### Execute ( )
>
> Draw the model immediately in the current state. Can be called multiple times
>
> Useful for stacking material effects

---

> ### DrawExtraPass ( )
>
> Redraws the model. Can be used to achieve various effects with different materials.
>
> I have never used this, as Execute works fine :p

---

> ### SetColorModulation ( red: integer, green: integer, blue: integer )
>
> Sets the color modulation of the model via RenderView. 
>
> This is probably what you should use to change the color of the model
>
> **All of the parameters use the range 0 to 1**

---

> #### StudioSetColorModulation ( red: integer, green: integer, blue: integer )
>
> Sets the color modulation of the model via StudioRender. Only works for models rendered using STUDIO_RENDER flag.
>
> **All of the parameters use the range 0 to 1**