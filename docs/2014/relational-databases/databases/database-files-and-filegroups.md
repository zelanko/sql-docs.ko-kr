---
title: 데이터베이스 파일 및 파일 그룹 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server], files
- filegroups [SQL Server]
- transaction logs [SQL Server], about
- transaction logs [SQL Server], files
- .mdf files
- data files [SQL Server]
- default filegroups
- files [SQL Server], about files and filegroups
- secondary files [SQL Server]
- log files [SQL Server]
- .ndf files
- files [SQL Server]
- .ldf files
- database files [SQL Server]
- databases [SQL Server], filegroups
- filegroups [SQL Server], types
- primary filegroups [SQL Server]
- user-defined filegroups [SQL Server]
- filegroups [SQL Server], about filegroups
- primary files [SQL Server]
- file types [SQL Server]
ms.assetid: 9ca11918-480d-4838-9198-cec221ef6ad0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3d75dee637a5579ca3f189e14333fbf9356623d0
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52790115"
---
# <a name="database-files-and-filegroups"></a>데이터베이스 파일 및 파일 그룹
  모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에는 최소한 두 개의 운영 체제 파일인 데이터 파일과 로그 파일이 있습니다. 데이터 파일은 테이블, 인덱스, 저장 프로시저 및 뷰 등의 개체와 데이터를 포함합니다. 로그 파일은 데이터베이스의 모든 트랜잭션을 복구하는 데 필요한 정보를 포함합니다. 데이터 파일은 할당 및 관리를 간편하게 수행하기 위해 파일 그룹으로 그룹화할 수 있습니다.  
  
## <a name="database-files"></a>데이터베이스 파일  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에는 다음 표에 설명된 것처럼 세 가지 유형의 파일이 있습니다.  
  
|파일|Description|  
|----------|-----------------|  
|주|주 데이터 파일은 데이터베이스의 시작 정보를 포함하며 데이터베이스의 나머지 파일을 가리킵니다. 사용자 데이터와 개체를 이 파일에 저장하거나 보조 데이터 파일에 저장할 수 있습니다. 모든 데이터베이스에는 하나의 주 데이터 파일이 있습니다. 권장되는 주 데이터 파일 확장명은 .mdf입니다.|  
|보조|보조 데이터 파일은 선택적으로 사용하는 사용자 정의 데이터 파일이며 사용자 데이터를 저장합니다. 보조 파일은 각 파일을 서로 다른 디스크 드라이브에 배치하여 데이터를 여러 디스크에 분산시키는 데 사용할 수 있습니다. 또한 데이터베이스가 단일 Windows 파일의 최대 크기를 초과할 경우 보조 데이터 파일을 사용하여 데이터베이스 크기를 계속해서 늘릴 수 있습니다.<br /><br /> 권장되는 보조 데이터 파일 확장명은 .ndf입니다.|  
|트랜잭션 로그|트랜잭션 로그 파일은 데이터베이스 복구에 사용되는 로그 정보를 저장합니다. 데이터베이스마다 최소한 하나의 로그 파일이 있어야 합니다. 권장되는 트랜잭션 로그 파일 확장명은 .ldf입니다.|  
  
 예를 들어 모든 데이터와 개체를 하나의 주 파일에 저장하고 트랜잭션 로그 정보를 로그 파일에 저장하는 **Sales** 라는 단순한 데이터베이스를 만들 수 있습니다. 또는 한 개의 주 파일과 5개의 보조 파일을 포함하는 **Orders** 라는 더 복잡한 데이터베이스를 만들 수도 있습니다. 데이터베이스 내의 데이터와 개체는 6개의 파일에 분산되고 트랜잭션 로그 정보는 4개의 로그 파일에 포함됩니다.  
  
 기본적으로 데이터와 트랜잭션 로그는 동일한 드라이브와 경로에 배치됩니다. 이것은 단일 디스크 시스템의 경우에 해당하며 프로덕션 환경에서는 최적이 아닐 수도 있습니다. 데이터와 로그 파일은 서로 다른 디스크에 배치하는 것이 좋습니다.  
  
## <a name="filegroups"></a>파일 그룹  
 모든 데이터베이스에는 주 파일 그룹이 한 개씩 있습니다. 주 파일 그룹은 주 데이터 파일과 다른 파일 그룹에 배치되지 않은 보조 파일을 포함합니다. 사용자 정의 파일 그룹을 만들어 데이터 파일을 그룹화함으로써 관리, 데이터 할당 및 배치를 간편하게 수행할 수 있습니다.  
  
 예를 들어 3개의 파일(Data1.ndf, Data2.ndf 및 Data3.ndf)을 3개의 디스크 드라이브에 하나씩 만들어서 **fgroup1**이라는 파일 그룹에 할당할 수 있습니다. 그런 다음 **fgroup1**파일 그룹에 한 개의 테이블을 만들 수 있습니다. 이렇게 하면 해당 테이블의 데이터에 대한 쿼리가 3개의 디스크로 분산되므로 성능이 향상됩니다. RAID(Redundant Array of Independent Disks) 스트라이프 세트에 단일 파일을 만들어 사용해도 이와 동일한 수준으로 성능이 향상될 수 있습니다. 그러나 파일과 파일 그룹을 사용하면 새 디스크에 새 파일을 쉽게 추가할 수 있습니다.  
  
 모든 데이터 파일은 다음 표에 나열된 파일 그룹에 저장됩니다.  
  
|파일 그룹|Description|  
|---------------|-----------------|  
|주|주 파일을 포함하는 파일 그룹. 주 파일 그룹에는 모든 시스템 테이블이 할당됩니다.|  
|사용자 정의|사용자가 데이터베이스를 처음 만들 때 또는 나중에 수정할 때 만드는 파일 그룹|  
  
### <a name="default-filegroup"></a>기본 파일 그룹  
 데이터베이스에서 개체를 만들 때 어떤 파일 그룹에 속하는지 지정하지 않으면 기본 파일 그룹에 할당됩니다. 언제든지 정확하게 하나의 파일 그룹이 기본 파일 그룹으로 지정됩니다. 기본 파일 그룹의 파일은 다른 파일 그룹에 할당되지 않은 모든 새로운 개체를 보관할 수 있을 만큼 크기가 커야 합니다.  
  
 PRIMARY 파일 그룹은 ALTER DATABASE 문을 사용하여 변경하지 않으면 기본 파일 그룹입니다. 시스템 개체 및 테이블에 대한 할당은 새 기본 파일 그룹이 아니라 PRIMARY 파일 그룹에 남게 됩니다.  
  
## <a name="related-content"></a>관련 내용  
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)  
  
 [ALTER DATABASE 파일 및 파일 그룹 옵션&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options)  
  
 [데이터베이스 분리 및 연결&#40;SQL Server&#41;](database-detach-and-attach-sql-server.md)  
  
  
