[![ci](https://github.com/stardado/moodle-mod_reengagement/actions/workflows/ci.yml/badge.svg?branch=MOODLE_503_STABLE)](https://github.com/stardado/moodle-mod_reengagement/actions/workflows/ci.yml?branch=MOODLE_503_STABLE)

# Re-engagement plugin developed by Catalyst IT

Allows timed release of content and emails users to remind them to complete course activities

More documentation available here: https://docs.moodle.org/en/Reengagement_activity

About this fork
---------------
This is a fork of [catalyst/moodle-mod_reengagement](https://github.com/catalyst/moodle-mod_reengagement),
maintained to run the plugin on Moodle 5.0 - 5.3 until upstream publishes a branch for these versions.

The branch `MOODLE_503_STABLE` is based on upstream `MOODLE_405_STABLE` (commit `7a34c3f`, 2026-02-27).
The plugin code is unchanged; only the version metadata has been updated. If upstream releases a
Moodle 5.x branch, prefer that one.

Branches
--------
The git branches here support the following versions.

| Moodle version     | Branch      |
| ----------------- | ----------- |
| Moodle 4.5 - 5.3 | MOODLE_503_STABLE (this fork, default) |
| Moodle 4.5 | MOODLE_405_STABLE (upstream) |
| Moodle 4.4 | MOODLE_404_STABLE (upstream) |
| Moodle 4.0 - 4.3 | MOODLE_400_STABLE (upstream) |
| Totara 12 | TOTARA_12 (upstream) |

Installation
------------
Since Moodle 5.1 the web root is the `public` directory, so the plugin goes into `public/mod/reengagement`.
On Moodle 4.5 and 5.0 use `mod/reengagement` instead.

```bash
cd /path/to/moodle
git clone -b MOODLE_503_STABLE https://github.com/stardado/moodle-mod_reengagement.git public/mod/reengagement
sudo -u www-data php admin/cli/upgrade.php --non-interactive
```

Switching an existing upstream clone to this fork:

```bash
cd /path/to/moodle/public/mod/reengagement
git remote set-url origin https://github.com/stardado/moodle-mod_reengagement.git
git fetch origin
git checkout -B MOODLE_503_STABLE origin/MOODLE_503_STABLE
```

Then run `admin/cli/upgrade.php` or visit *Site administration > Notifications*.

Changes compared to upstream
----------------------------
### 2026100901 (2026100901-m53)
- `view.php`: replaced the Bootstrap 4 class `form-inline` (removed with Bootstrap 5 in Moodle 5.0) in the bulk
  actions bar with flex utilities, taken from upstream PR [#214](https://github.com/catalyst/moodle-mod_reengagement/pull/214).
- Moodle coding style fixed with phpcbf (no functional changes).
- CI: release job and PR version bump check disabled for the fork, manual runs enabled. Additional workflow
  `moodle-plugin-ci.yml` tests against MOODLE_503_STABLE with moodlehq/moodle-plugin-ci (PHP 8.3/pgsql 17,
  PHP 8.4/MariaDB 11.4).

### 2026100900 (2026100900-m53)
- `version.php`: supported range set to Moodle 4.5 - 5.3 (`[405, 503]`), version bumped to `2026100900`
  so it installs as an upgrade over earlier local builds (e.g. `2026030600-m51`).
- Checked against the API changes of Moodle 5.2 and 5.3 listed in `UPGRADING.md`: the removed `checkall()`
  JavaScript function is not used (only an element id of that name, handled by `core_user/participants`),
  no deprecated `user/lib.php` or `external_*` functions are called, the `core_user/participants` and
  `core_user/status_field` AMD modules are unchanged.
- All classes load without debugging notices on Moodle 5.3 (Build 20261005).

License
-------
GNU GPL v3 or later, see the file headers. Original work © Catalyst IT.
