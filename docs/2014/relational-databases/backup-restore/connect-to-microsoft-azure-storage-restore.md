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
manager: craigg
ms.openlocfilehash: 6fbb57fe629797e34cc7c61f224d65d46d4e66cd
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154769"
---
# <a name="connect-to-azure-storage-restore"></a>Azure Storage에 연결 (복원)
  이 대화 상자에서는 azure storage 계정에서 파일 저장소를 검색 하기 위해 Azure storage 계정 정보에 대 한 연결을 지정할 수 있습니다. 필요한 정보를 지정한 후 **연결** 을 클릭 하 여 Azure storage에 대 한 연결을 설정 합니다.  
  
## <a name="azure-storage-account"></a>Azure Storage 계정  
 **저장소 계정**  
 사용 하려는 Azure storage 계정의 이름을 선택 하거나 입력 하거나 붙여 넣습니다. 드롭다운 상자에 이전에 사용한 계정이 나열됩니다.  
  
 **계정 키**  
 Azure 저장소 계정 액세스 키를 지정 합니다.  
  
 **보안 엔드포인트 사용(HTTPS)** 확인란  
 Azure storage에 대 한 보안 연결을 설정 하려면이 옵션을 선택 합니다 (권장).  
  
 **계정 키 저장** 확인란  
 SQL Server에서 이 스토리지 계정에 대한 액세스 키를 기억하도록 설정하려면 이 확인란을 선택합니다.  
  
### <a name="sql-credential"></a>SQL 자격 증명  
 **기존 자격 증명 선택**  
 스토리지 계정 및 계정 키 정보와 일치하는 기존 SQL 자격 증명을 선택합니다.  
  
 **새 자격 증명 만들기**  
 스토리지 계정 및 계정 키 정보를 사용하여 새 자격 증명을 만들려면 이 옵션을 선택합니다. **자격 증명 이름** 필드에서 새 자격 증명 이름을 지정합니다.  
  
  
