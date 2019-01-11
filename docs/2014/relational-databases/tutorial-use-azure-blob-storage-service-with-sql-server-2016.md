---
title: '자습서: Windows Azure Storage 서비스에서 SQL Server 데이터 파일 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: e69be67d-da1c-41ae-8c9a-6b12c8c2fb61
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e3d33209cd6dfe261a5deced345adac70b46961f
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52810975"
---
# <a name="tutorial-sql-server-data-files-in-windows-azure-storage-service"></a>자습서: Microsoft Azure Storage의 SQL Server 데이터 파일 서비스
  Windows Azure 스토리지 서비스의 SQL Server 데이터 파일 자습서를 시작합니다. 이 자습서는 Windows Azure BLOB 스토리지 서비스에서 SQL Server 데이터 파일을 저장하는 방법을 이해하도록 도와 줍니다.  
  
 Windows Azure BLOB 스토리지 서비스에 SQL Server를 통합할 수 있도록 지원하는 기능은 SQL Server 2014에서 새로 도입되었습니다. 참조 된 기능의 개요와이 기능을 사용할 때의 이점에 대 한 [Windows Azure의 SQL Server 데이터 파일](databases/sql-server-data-files-in-microsoft-azure.md)합니다.  
  
## <a name="what-you-will-learn"></a>학습 내용  
 이 자습서에서는 Windows Azure 스토리지 서비스에서 SQL Server 데이터 파일을 저장하는 방법을 여러 섹션을 통해 보여 줍니다. 각 단원은 특정 태스크에 초점을 맞추고 있습니다. 먼저, Windows Azure에서 스토리지 계정 및 컨테이너를 만드는 방법을 살펴봅니다. 그런 다음 Windows Azure 스토리지에 SQL Server를 통합할 수 있도록 SQL Server 자격 증명을 만드는 방법을 살펴봅니다. 그런 다음 Windows Azure 스토리지에서 직접 데이터베이스를 만듭니다. 또한 이 자습서에서는 암호화, 마이그레이션, 백업 및 복원 시나리오를 보여 줍니다.  
  
 이 자습서는 다음 9개의 단원으로 구성되어 있습니다.  
  
 **[1 단원: Windows Azure 저장소 계정 및 컨테이너 만들기](../tutorials/lesson-1-create-windows-azure-storage-account-and-container.md)**  
 이 단원에서는 Windows Azure 스토리지 계정 및 컨테이너를 만듭니다.  
  
 **[2 단원입니다. 컨테이너에 정책을 만들고 공유 액세스 서명 생성 &#40;SAS&#41; 키](lesson-1-create-stored-access-policy-and-shared-access-signature.md)**  
 이 단원에서는 BLOB 컨테이너에서 정책을 만들고 공유 액세스 서명을 생성합니다.  
  
 **[3 단원: SQL Server 자격 증명 만들기](lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)**  
 이 단원에서는 Windows Azure 스토리지 계정에 액세스하는 데 사용하는 보안 정보를 저장하는 자격 증명을 만들 수 있습니다.  
  
 **[4 단원: Windows Azure Storage에서 데이터베이스 만들기](../relational-databases/lesson-3-database-backup-to-url.md)**  
 이 단원에서는 CREATE Database FILENAME 옵션을 사용하여 Windows Azure 스토리지에서 데이터베이스를 만듭니다.  
  
 **[5 단원입니다. &#40;옵션&#41; TDE를 사용 하 여 데이터베이스를 암호화 합니다.](../relational-databases/lesson-4-restore-database-to-virtual-machine-from-url.md)**  
 이 단원에서는 TDE(투명한 데이터 암호화)와 서버 인증서를 사용하여 데이터베이스를 암호화합니다.  
  
 **[6 단원: 원본에서 데이터베이스를 마이그레이션할 컴퓨터 온-프레미스를 대상 컴퓨터에 Windows Azure](lesson-5-backup-database-using-file-snapshot-backup.md)**  
 이 단원에서는 CREATE DATABASE FOR ATTACH 옵션을 사용하여 온-프레미스에서 Microsoft Azure의 가상 머신으로 데이터베이스를 마이그레이션합니다.  
  
 **[7 단원: Windows Azure Storage로 데이터 파일 이동](../relational-databases/lesson-6-generate-activity-and-backup-log-using-file-snapshot-backup.md)**  
 이 단원에서는 ALTER DATABASE 문을 사용하여 Windows Azure 스토리지로 데이터 파일을 이동합니다.  
  
 **[8단원. Windows Azure Storage에 데이터베이스를 복원 합니다.](../relational-databases/lesson-7-restore-a-database-to-a-point-in-time.md)**  
 이 단원에서는 RESTORE Database MOVE 옵션을 사용하여 Windows Azure 스토리지로 데이터베이스를 복원합니다.  
  
 **[9 단원입니다. Windows Azure Storage에서 데이터베이스 복원](lesson-8-restore-as-new-database-from-log-backup.md)**  
 이 단원에서는 RESTORE Database MOVE 옵션을 사용하여 Windows Azure 스토리지에서 데이터베이스를 복원합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Windows Azure의 SQL Server 데이터 파일](databases/sql-server-data-files-in-microsoft-azure.md)  
  
  
