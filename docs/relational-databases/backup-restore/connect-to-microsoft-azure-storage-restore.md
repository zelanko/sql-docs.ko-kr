---
title: Microsoft Azure Storage에 연결(복원) | Microsoft 문서
description: SQL Server에서 Azure Storage 계정 대화 상자를 사용하여 Azure 계정의 파일 스토리지를 가져오도록 Azure Storage 계정 정보에 대한 연결을 지정할 수 있습니다.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.restore.connectstorage.f1
ms.assetid: c0b7d7c8-b878-4b7f-8120-d0c6917b583f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 7c6564d9dc63a4d2e35ac306db91cead15f024c6
ms.sourcegitcommit: 9afb612c5303d24b514cb8dba941d05c88f0ca90
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/28/2020
ms.locfileid: "82220460"
---
# <a name="connect-to-microsoft-azure-storage-restore"></a>Microsoft Azure 스토리지에 연결(복원)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  대화 상자를 사용하면 Azure Storage 계정에서 파일 스토리지를 검색하기 위해 Azure Storage 계정 정보에 대한 연결을 지정할 수 있습니다. 필요한 정보를 지정한 후 **연결**을 클릭하여 Azure Storage에 대한 연결을 설정합니다.  
  
## <a name="azure-storage-account"></a>Azure Storage 계정  
 **스토리지 계정**  
 사용할 Azure Storage 계정 이름을 선택, 입력 또는 붙여 넣습니다. 드롭다운 상자에 이전에 사용한 계정이 나열됩니다.  
  
 **계정 키**  
 Azure Storage 계정 액세스 키를 지정합니다.  
  
 **보안 엔드포인트 사용(HTTPS)** 확인란  
 Azure Storage에 대한 보안 연결을 설정하려면 이 옵션을 선택합니다(권장 사항).  
  
 **계정 키 저장** 확인란  
 SQL Server에서 이 스토리지 계정에 대한 액세스 키를 기억하도록 설정하려면 이 확인란을 선택합니다.  
  
### <a name="sql-credential"></a>SQL 자격 증명  
 **기존 자격 증명 선택**  
 스토리지 계정 및 계정 키 정보와 일치하는 기존 SQL 자격 증명을 선택합니다.  
  
 **새 자격 증명 만들기**  
 스토리지 계정 및 계정 키 정보를 사용하여 새 자격 증명을 만들려면 이 옵션을 선택합니다. **자격 증명 이름** 필드에서 새 자격 증명 이름을 지정합니다.  
  
  
