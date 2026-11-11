# UI layout and spacing

When designing or implementing a UI, separate layout from content and individual control styling. Put shared rules for grids, page and section composition, alignment, wrapping, responsive behavior and spacing between elements in reusable layout primitives or composition components. Screens and feature code place content into those containers and select supported layout variants; they should not repeatedly assign individual margins or recreate the same positioning rules for each element.

Layout containers own the spacing and alignment of their immediate children; UI components own their internal padding and arrangement. Use the project's shared spacing scale and consistent defaults so adding, removing or reordering content preserves the layout contract without neighbor-specific adjustments. Define responsive wrapping, minimum widths and overflow at the responsible container rather than relying on accidental text wrapping or page-wide overflow. Make genuinely specialized layouts explicit and keep their rules with the composition that owns them.

Use consistent horizontal insets to align headings, metadata, controls and body content that belong to the same panel. Let the component own edge padding and let the parent layout set gaps between siblings. Use smaller gaps within related groups and larger gaps between groups to make hierarchy visible. Choose these values from the project's existing scale.

Let panels size to their content when equal heights add no value. When a chart would show only zeros, use a compact message for the selected scope or period and preserve access to the underlying values, such as through an existing table. Distinguish a valid zero result from loading, unavailable or stale data.

Reuse the selected framework or component kit's layout capabilities before adding wrappers or dependencies. Introduce only the smallest reusable layer needed to hide repeated layout decisions; do not require a universal grid framework, particular component names, library or fixed spacing values. Preserve project conventions, explicit visual decisions and component accessibility. A spacing scale alone does not replace layout composition, and abstraction alone does not prove visual quality: verify representative screens with long content, relevant viewport sizes and UI states through the project's authorized visual verification method.

Apply [shared/local adoption](adoption.md) when introducing or updating these conventions.
