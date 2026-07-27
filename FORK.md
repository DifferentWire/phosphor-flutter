# Fork note — why DifferentWire maintains this

This is a fork of [`phosphor-icons/phosphor-flutter`](https://github.com/phosphor-icons/phosphor-flutter) (MIT license, preserved).

## The problem

Flutter **3.44** marked `IconData` as a **`final` class** — it can no longer be extended or implemented outside its own library. Upstream `phosphor_flutter` (latest published: 2.1.0) is built entirely on:

```dart
class PhosphorIconData extends IconData { ... }
```

so it **fails to compile on Flutter 3.44+**:

```
Error: The class 'IconData' can't be extended outside of its library because it's a final class.
```

As of this fork's creation there was **no published upstream release compatible with 3.44**, which blocked DifferentWire apps from upgrading to Flutter 3.44.

## The patch

Rework the icon data so accessors and per-style constants return **plain `IconData`** instead of the (now-illegal) `IconData` subclasses:

- Style files (`regular`/`bold`/`fill`/`light`/`thin`/`duotone`): each constant is now
  `IconData(codePoint, fontFamily: 'Phosphor<Style>', fontPackage: 'phosphor_flutter', matchTextDirection: true)`.
- `phosphor_icons_base.dart`: accessor return types `PhosphorIconData` → `IconData`.
- Removed the `extends IconData` classes and the dead `phosphor_icon_data.dart` export.
- `PhosphorIcon` widget: dropped the duotone secondary-layer branch (**duotone now renders single-layer**).

### Compatibility
- **Public API is unchanged** for the common case: `PhosphorIcons.name([style])` still works and returns an `IconData` usable in `Icon(...)` / anywhere `IconData` is expected. Consumers using icons as `IconData` need **no changes**.
- **Breaking:** the `PhosphorIconData` / `PhosphorFlatIconData` / `PhosphorDuotoneIconData` **types are gone**, and **duotone loses its second layer**. If you referenced those types directly or relied on duotone's two-tone rendering, that won't carry over. (DifferentWire consumers do neither.)

## Retirement plan

This fork exists only until upstream ships a 3.44-compatible release.

1. Offer the fix (or an equivalent) to upstream as a PR.
2. When upstream publishes a compatible version, repoint consumers' `pubspec.yaml` back at pub.dev.
3. Archive this repo.

Tracking: `DifferentWire/Unfocused#1237`.
