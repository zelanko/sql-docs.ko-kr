---
title: '자습서: Azure Storage 서비스의 SQL Server 데이터 파일 | Microsoft Docs'
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
ms.openlocfilehash: 89022104fef0b99412060290361961922b9d6b08
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155313"
---
# <a name="tutorial-sql-server-data-files-in-azure-storage-service"></a>자습서: Azure Storage 서비스에서 데이터 파일 SQL Server
  Azure Storage Service의 SQL Server 데이터 파일 자습서를 시작 합니다. 이 자습서는 Azure Blob 저장소 서비스에 SQL Server 데이터 파일을 직접 저장 하는 방법을 이해 하는 데 도움이 됩니다.  
  
 Azure Blob storage 서비스에 대 한 SQL Server 통합 지원은 SQL Server 2014 향상 된 기능입니다. 이 기능을 사용 하는 기능 및 이점에 대 한 개요는 [Azure의 SQL Server 데이터 파일](databases/sql-server-data-files-in-microsoft-azure.md)을 참조 하세요.  
  
## <a name="what-you-will-learn"></a>학습 내용  
 이 자습서에서는 여러 단원에서 Azure Storage 서비스에 SQL Server 데이터 파일을 저장 하는 방법을 보여 줍니다. 각 단원은 특정 태스크에 초점을 맞추고 있습니다. 먼저 Azure에서 저장소 계정 및 컨테이너를 만드는 방법을 알아봅니다. 그런 다음 SQL Server Azure Storage와 통합할 수 있도록 SQL Server 자격 증명을 만드는 방법에 대해 알아봅니다. 그런 다음 Azure Storage에서 직접 데이터베이스를 만듭니다. 또한 이 자습서에서는 암호화, 마이그레이션, 백업 및 복원 시나리오를 보여 줍니다.  
  
 이 자습서는 다음 9개의 단원으로 구성되어 있습니다.  
  
 **[1 단원: Azure Storage 계정 및 컨테이너 만들기](../tutorials/lesson-1-create-windows-azure-storage-account-and-container.md)**  
 이 단원에서는 Azure Storage 계정과 컨테이너를 만듭니다.  
  
 **[2 단원. 컨테이너에서 정책을 만들고 공유 액세스 서명 &#40;SAS&#41; 키 생성](lesson-1-create-stored-access-policy-and-shared-access-signature.md)**  
 이 단원에서는 BLOB 컨테이너에서 정책을 만들고 공유 액세스 서명을 생성합니다.  
  
 **[3 단원: SQL Server 자격 증명 만들기](lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)**  
 이 단원에서는 Azure 스토리지 계정에 액세스하는 데 사용하는 보안 정보를 저장하는 자격 증명을 만들 수 있습니다.  
  
 **[4 단원: Azure Storage에서 데이터베이스 만들기](../relational-databases/lesson-3-database-backup-to-url.md)**  
 이 단원에서는 CREATE Database FILENAME 옵션을 사용 하 여 Azure Storage에서 데이터베이스를 만듭니다.  
  
 **5 단원. &#40;Tde를 사용 하 여 데이터베이스 암호화 (옵션)&#41;**  
 이 단원에서는 TDE(투명한 데이터 암호화)와 서버 인증서를 사용하여 데이터베이스를 암호화합니다.  
  
 **[6 단원: 온-프레미스의 원본 컴퓨터에서 Azure의 대상 컴퓨터로 데이터베이스 마이그레이션](lesson-5-backup-database-using-file-snapshot-backup.md)**  
 이 단원에서는 CREATE DATABASE FOR ATTACH 옵션을 사용 하 여 온-프레미스에서 Azure의 가상 머신으로 데이터베이스를 마이그레이션합니다.  
  
 **[7 단원: Azure Storage으로 데이터 파일 이동](../relational-databases/lesson-6-generate-activity-and-backup-log-using-file-snapshot-backup.md)**  
 이 단원에서는 ALTER DATABASE 문을 사용 하 여 데이터 파일을 Azure Storage로 이동 합니다.  
  
 **[8단원. Azure Storage로 데이터베이스 복원](../relational-databases/lesson-7-restore-a-database-to-a-point-in-time.md)**  
 이 단원에서는 RESTORE Database MOVE 옵션을 사용 하 여 Azure Storage 데이터베이스로 데이터베이스를 복원 합니다.  
  
 **[단원 9. Azure Storage에서 데이터베이스 복원](lesson-8-restore-as-new-database-from-log-backup.md)**  
 이 단원에서는 RESTORE Database MOVE 옵션을 사용 하 여 Azure Storage에서 데이터베이스를 복원 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Azure에서 데이터 파일 SQL Server](databases/sql-server-data-files-in-microsoft-azure.md)  
  
  
