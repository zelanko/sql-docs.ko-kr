---
title: Azure Storage에 연결 (복원) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.restore.connectstorage.f1
ms.assetid: c0b7d7c8-b878-4b7f-8120-d0c6917b583f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 9fb4a8943c237e37ca612bf367abe99d47c8eb08
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84958788"
---
# <a name="connect-to-azure-storage-restore"></a>Azure Storage에 연결(복원)
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
  
  
