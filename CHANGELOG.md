# Changelog

## [Unreleased]

### Added

- Added `PartialEq` impls for `CStr16 == CStr16`, `&CStr16 == CString`,
  and `CString == &CStr16`.
- Added `Display` impl for `CString16`.
- Added `Handle::from_ptr` and `SystemTable<View>::from_ptr`, which are
  `unsafe` methods for initializing from a raw pointer.
- Added `CStr16::as_slice_with_nul` to provide immutable access to the
  underlying slice.

### Changed

- `File::open` now takes the filename as `&CStr16` instead of `&str`,
  avoiding an implicit string conversion.
- `FileInfo::new`, `FileSystemInfo::new`, and
  `FileSystemVolumeLabel::new` now take their `name` parameter as
  `&CStr16` instead of `&str`, avoiding an implicit string conversion.

### Removed

- Removed `CStr16::as_string` method. Use
  [`ToString`](https://doc.rust-lang.org/alloc/string/trait.ToString.html)
  instead.
- Removed `FileInfoCreationError::InvalidChar`. This error type is no
  longer needed due to the removal of implicit string conversions in
  file info types.

### Fixed

- Fixed compilation with Rust 1.60 by no longer enabling the
  `vec_spare_capacity` feature, which has been stabilized.
- Fixed the header size calculated by `FileInfo::new` and
  `FileSystemInfo::new`.