Debian Trixie - LedgerSMB 1.13.4 Branch

#1
- Forked LedgerSMB and added upstream remote
- Created branch `debian-trixie-1.13.4` from tag `1.13.4`
- Installed Perl dependencies with `cpanm --installdeps .`
- Perl modules were installed into `~/perl5`
- PSGI entry file confirmed as `bin/ledgersmb-server.psgi`
- Startup initially failed because `LedgerSMB::Setting` was not found
- Confirmed `Setting.pm` exists in `old/lib/LedgerSMB/Setting.pm`
- Successful startup required both `lib` and `old/lib` in `@INC`
- Startup then failed on JSON backend compatibility
- Installed `Cpanel::JSON::XS` and retried
- Backend then started successfully with `plackup`
- Browser showed raw webpack template instead of UI
- Confirmed frontend project is in `UI/`
- Installed Node dependencies with `npm install --legacy-peer-deps`
- Built frontend successfully with `npm run build`
- LedgerSMB login screen now loads successfully via localhost
- Current state: login page visible with fields for username, password, and company
- Next step: PostgreSQL database setup

#0

- Fresh environment: Debian 13 (Trixie) XFCE 
- Perl 5.40 
- No LedgerSMB 1.13.4 installed

