---
title: SQL Server 오류 로그 구성 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.configurelogs.configureerrorlogs.f1
ms.assetid: 03f0d463-9b0b-4af9-a853-da936d75e5af
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 21737a329fdd6bf68f1bf7df5f4df4511b26cfd9
ms.sourcegitcommit: 36c3ead6f2a3628f58040acf47f049f0b0957b8a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/30/2019
ms.locfileid: "71688320"
---
# <a name="scm-services---configure-sql-server-error-logs"></a>SCM 서비스 - SQL Server 오류 로그 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그의 재활용 방법을 확인하거나 수정하는 방법에 대해 설명합니다.  

## <a name="to-open-the-configure-sql-server-error-logs-dialog-box"></a>SQL Server 오류 로그 구성 대화 상자를 열려면  

1. 개체 탐색기에서 SQL Server 인스턴스를 확장하고 **관리**를 확장한 다음 **SQL Server 로그**를 마우스 오른쪽 단추로 클릭하고 **구성**을 클릭합니다.

2. **SQL Server 오류 로그 구성** 대화 상자의 다음 옵션 중에서 선택합니다.

    1\. 로그 파일 개수

      **재활용 이전의 오류 로그 파일 수 제한**

      재활용하기 전의 오류 로그 수 제한을 두려면 선택합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 시작할 때마다 오류 로그가 새로 만들어집니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 최근 6개 로그의 백업을 보관합니다.  
  
      **최대 오류 로그 파일 수**

      재활용하기 전의 오류 로그 파일 최대 개수를 지정합니다. 기본값은 6으로, 현재 로그 1개와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 백업 로그를 재활용하기까지 유지하는 이전 백업 로그 5개입니다.

    2\. 로그 파일 크기

      **오류 로그 파일의 최대 크기(KB)**

      각 파일의 크기(KB)를 설정할 수 있습니다. 0으로 두는 경우 로그 크기는 무제한입니다.
