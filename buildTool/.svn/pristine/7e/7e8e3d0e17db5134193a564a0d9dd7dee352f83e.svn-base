@echo off
::%1 build_Project, options are: S2DE, EDVR, Berthing, MMR, All NTDPS Integration Deliverables
::%2 svn.username
::%3 svn.pass
::%4 is_si: true or false for silent build, this will be set to true when doing nightly builds


set root=C:\working\buildTool
CD /D %root%

ant -Dbuild_Project="%1" -Dsvn_user_name="%2" -Dsvn_pass=%3 -Dis_si=%4 2>&1