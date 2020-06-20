---
title: 자격 증명 만들기 - Azure Storage 인증 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.backuptourl.createcred.f1
ms.assetid: 0622619d-27c5-4ff0-83e5-cde31648c27a
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 5f76a455637e28c06e967b0609cea19a874d7967
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84958593"
---
# <a name="create-credential---authenticate-to-azure-storage"></a>자격 증명 만들기 - Azure 스토리지 인증
  **URL로 백업 - 자격 증명 만들기** 대화 상자를 사용하여 새 SQL 자격 증명을 만듭니다.  
  
 이 대화 상자를 사용하여 자격 증명을 만들 때 로컬 인증서 저장소에 추가된 Azure 관리 인증서 또는 컴퓨터에 다운로드된 게시 프로필을 제공하여 구독 및 스토리지 계정 정보의 유효성을 검사해야 합니다.  
  
 **SQL 자격 증명**  
 만들려는 SQL 자격 증명의 이름을 지정합니다.  
  
## <a name="azure-credentials"></a>Azure 자격 증명  
 **관리 인증서**  
 이 옵션을 사용하여 Azure의 관리 인증서와 일치하는 로컬 인증서 저장소의 인증서를 지정합니다. Azure 관리 인증서에 대한 자세한 내용은 [Azure용 관리 인증서 만들기 및 업로드](https://go.microsoft.com/fwlink/?LinkId=320781)를 참조하세요.  
  
 **구독**  
 로컬 인증서 저장소의 관리 인증서와 일치하는 Azure 구독 ID를 선택, 입력 또는 붙여 넣습니다.  
  
 **게시 프로필**  
 게시 프로필을 컴퓨터에 다운로드한 경우 이 옵션을 사용합니다. 이 옵션을 사용하는 경우 구독 ID 및 인증서가 자동으로 채워집니다.  
  
> [!CAUTION]  
>  SQL Server는 현재 프로필 버전 2.0 게시를 지원합니다. 게시 프로필의 지원되는 버전을 다운로드하려면 [게시 프로필 2.0 다운로드](https://go.microsoft.com/fwlink/?LinkId=396421)를 참조하세요.  
  
## <a name="storage-account"></a>스토리지 계정  
 백업 파일을 저장하는 데 사용할 스토리지 계정을 선택합니다.  
  
  
