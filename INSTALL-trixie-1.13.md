# LedgerSMB 1.13.4 — Debian Trixie Installation and Observation

## Base setup
- Forked from the official LedgerSMB repository
- Local working repository: `~/LedgerSMB`
- Branch: `debian-trixie-1.13.4`
- Based on LedgerSMB tag: `1.13.4`
- Target system: Debian Trixie

## Purpose
This document records the installation and compatibility steps for running LedgerSMB 1.13.4 on Debian Trixie.

## Initial repository setup
- Added `upstream` remote pointing to the official LedgerSMB repository
- Fetched upstream branches and tags
- Created branch `debian-trixie-1.13.4` from tag `1.13.4`

## Installation steps

## Perl dependencies
```bash
cd ~/LedgerSMB
cpanm --installdeps .
```
- Modules were installed under ~/perl5
- Load local Perl library before starting LedgerSMB:
```bash
eval $(perl -I ~/perl5/lib/perl5 -Mlocal::lib)
```

##PSGI startup
- LedgerSMB 1.13.4 requires both lib and old/lib in the Perl include path.
- LedgerSMB::Setting is located at old/lib/LedgerSMB/Setting.pm
- start command:
```bash
cd ~/LedgerSMB
eval $(perl -I ~/perl5/lib/perl5 -Mlocal::lib)
plackup -I lib -I old/lib -p 5000 bin/ledgersmb-server.psgi
```

##JSON compatibility
- Startup failed initially with a JSON backend error.
- Installed:
```bash
cpanm --notest Cpanel::JSON::XS
```

##Frontend build
- The backend started before the frontend was built, which caused a blank page showing raw webpack template tags.
- Install Node dependencies:
```bash
cd ~/LedgerSMB/UI
npm install --legacy-peer-deps
```

- build frontend:
```bash
npm run build
```

- npm install completed with warnings and reported vulnerabilities
- Do not run npm audit fix or npm audit fix --force at this stage
- Frontend build completed successfully despite warnings
