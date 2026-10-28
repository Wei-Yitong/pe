# Duplicate report

The Word document contains 31 embedded photo occurrences. Four repeated-photo groups have been consolidated into 27 primary figures. Rotation, resizing, and JPEG re-encoding can change bytes, so these groups were also checked visually rather than identified by file hash alone.

| Word duplicate group | Retained figure | Decision |
| --- | --- | --- |
| image4 + image9 | F04 | Retain image9, the higher-pixel-count version; the other occurrence is rotated. |
| image5 + image20 | F05 | Retain image5, the higher-resolution version; the other occurrence is rotated/resized. |
| image15 + image22 | F14 | Use IMG_1465.jpeg once; both occurrences show the annotated 24 V cable 2 photo. |
| image19 + image31 | F18 | Use IMG_1471.jpeg once; both occurrences show the same cable-routing photo. |

## GitHub upload

All 32 IMG_*.jpeg files were compared by SHA-256 and by the SHA-256 of decoded, EXIF-oriented RGB pixel data. Neither comparison found identical files. Visual comparison distinguishes annotated versions and different viewpoints.

- IMG_1443.jpeg and IMG_1444.jpeg depict the same original AUX12V OUT photo, but IMG_1444.jpeg includes added wiring annotations. Keep both: S01 is the full-resolution unannotated original, F25 is the annotated version.
- IMG_1451.jpeg and IMG_1471.jpeg show different views of the same area; they are not duplicate captures. Keep both.
- Other additional views are retained as supplementary figures rather than discarded for showing the same equipment.
- The unrelated landscape image, README, and placeholder files are not referenced by the wiring documentation.

The repository edition reuses existing GitHub photos instead of storing duplicate copies. Only five Word-only image files are added. Four repeated-photo groups are consolidated in the reading copy; all source photos remain intact. The earlier extensionless, incomplete text document is replaced by the complete Markdown and ASCII editions.
