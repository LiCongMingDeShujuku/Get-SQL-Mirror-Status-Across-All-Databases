![CLEVER DATA GIT REPO](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/0-clever-data-github.png "李聪明的数据库")

# 获取所有数据库的SQL镜像状态
#### Get SQL Mirror Status Across All Databases
**发布-日期: 2015年08月27日 (评论)**

![#](images/##############?raw=true "#")

## Contents

- [中文](#中文)
- [English](#English)
- [SQL Logic](#Logic)
- [Build Info](#Build-Info)
- [Author](#Author)
- [License](#License) 


## 中文
使用此逻辑可以跨所有数据库获取镜像状态。


## English
Use this logic to get the Mirrored Status across all databases.

---
## Logic
```SQL
use master;
set nocount on
declare @get_database_mirroring_state varchar(max)
set @get_database_mirroring_state = ''
select @get_database_mirroring_state = @get_database_mirroring_state + 'declare @monitorresults_' + cast(database_id as varchar(2)) + ' as table (
database_name varchar(255)
, role int
, mirror_state tinyint
, witness_status tinyint
, log_generat_rate int
, unsent_log int
, sent_rate int
, unrestored_log int
, recovery_rate int
, transaction_delay int
, transaction_per_sec int
, average_delay int
, time_recorded datetime
, time_behind datetime
, local_time datetime
);
insert into @monitorresults_' + cast(database_id as varchar(2)) + ' exec msdb..sp_dbmmonitorresults
@database_name = ''' + upper(DB_NAME(database_id)) + '''
, @mode = 0
, @update_table = 0;
select
''server'' = upper(@@servername)
, database_name
, ''role'' =
case role
when ''1'' then ''Principal''
when ''2'' then ''Mirror''
end
, average_delay
, ''mirror_state'' =
case mirror_state
when ''0'' then ''Suspended''
when ''1'' then ''Disconnected''
when ''2'' then ''Synchronizing''
when ''3'' then ''Pending Failover''
when ''4'' then ''Synchronized''
end


```



[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

- **李聪明的数据库 Lee's Clever Data**
- **Mike的数据库宝典 Mikes Database Collection**
- **李聪明的数据库** "Lee Songming"

[![Gist](https://img.shields.io/badge/Gist-李聪明的数据库-<COLOR>.svg)](https://gist.github.com/congmingshuju)
[![Twitter](https://img.shields.io/badge/Twitter-mike的数据库宝典-<COLOR>.svg)](https://twitter.com/mikesdatawork?lang=en)
[![Wordpress](https://img.shields.io/badge/Wordpress-mike的数据库宝典-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)

---
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Lee Songming](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/1-clever-data-github.png "李聪明的数据库")

