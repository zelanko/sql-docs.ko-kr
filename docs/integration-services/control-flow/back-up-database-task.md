---
description: 데이터베이스 백업 태스크
title: 데이터베이스 백업 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.backupdatabasetask.f1
helpviewer_keywords:
- database backups [Integration Services]
- Back Up Database task [Integration Services]
- backing up databases [Integration Services]
- transaction log backups [Integration Services]
- backing up transaction logs [Integration Services]
ms.assetid: b8839d71-13b7-41f2-a434-cb95020e79d7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 291a9fd0e0138eeb7b304e673f404163217f9ae5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88431075"
---
# <a name="back-up-database-task"></a>데이터베이스 백업 태스크

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  데이터베이스 백업 태스크는 여러 가지 유형의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 백업을 수행합니다. 자세한 내용은 [SQL Server Database 백업 및 복원](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)을 참조하세요.  
  
 데이터베이스 백업 태스크를 사용하면 패키지가 단일 데이터베이스나 여러 데이터베이스를 백업할 수 있습니다. 태스크에서 단일 데이터베이스만 백업하는 경우 데이터베이스 또는 데이터베이스 파일과 파일 그룹 등의 백업 구성 요소를 선택할 수 있습니다.  
  
## <a name="supported-recover-models-and-backup-types"></a>지원되는 복구 모델 및 백업 유형  
 다음 표에서는 데이터베이스 백업 태스크가 지원하는 복구 모델과 백업 유형을 나열합니다.  
  
|복구 모델|데이터베이스|데이터베이스 - 차등|트랜잭션 로그|파일 또는 파일 차등|  
|--------------------|--------------|---------------------------|---------------------|-------------------------------|  
|단순|필수|옵션|지원되지 않음|지원되지 않음|  
|전체|필수|옵션|필수|옵션|  
|대량 로그|필수|옵션|필수|옵션|  
  
 데이터베이스 백업 태스크는 Transact-SQL BACKUP 문을 캡슐화합니다. 자세한 내용은 [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)을 참조하세요.  
  
## <a name="configuration-of-the-back-up-database-task"></a>데이터베이스 백업 태스크 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 속성을 설정할 수 있습니다. 이 태스크는 **디자이너의** 도구 상자 **에 있는** 유지 관리 계획 태스크 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 섹션에서 수행할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목을 클릭하십시오.  
  
-   [데이터베이스 백업 태스크&#40;유지 관리 계획&#41;](../../relational-databases/maintenance-plans/options-in-the-back-up-database-task-for-maintenance-plan.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
  
