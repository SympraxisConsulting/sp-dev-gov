---
title: Loading arbitrary scripts in SharePoint Framework components
audience: Developer, Administrator, Architect
product-major: SharePoint
product-minor: NA
glossary-links: SPFx, No-script site
---

# Loading arbitrary scripts in SharePoint Framework components

## Summary

If your SharePoint Framework component allows users to specify an additional piece of script to load on the page, set the `requiresCustomScript` property in the component's property to `true`.

## Main Content

If a SharePoint Framework component allows users to configure an additional piece of script to load on the page, that component should have in its manifest the `requiresCustomScript` property set to `true`. In older versions of the SharePoint Framework, this property was named `safeWithCustomScriptDisabled` and developers would set it to `false` in case they allowed loading arbitrary scripts.

Setting the `requiresCustomScript` property to `true` in the manifest indicates, that there might be an additional risk using that particular component. Such component would not work on a site where using custom scripts is disabled (also referred to as a 'no-script site').

Using this property allows organizations to enforce the governance of customizations in their tenants and is a recommended good practice to follow.

**Important:** it is up to the developers, to use the `requiresCustomScript` property to indicate that a component allows loading custom scripts. If their solution allows loading custom scripts, but the `requiresCustomScript` property is set to `false` the solution will work just fine.