---
title: SSRS(SQL Server Reporting Services)의 제품 키 찾기 | Microsoft Docs
description: 프로덕션 환경에 서버를 설치할 수 있도록 SSRS(SQL Server Reporting Services) 2017 및 2019의 제품 키를 찾는 방법을 알아봅니다.
ms.date: 12/04/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.custom: seo-lt-2019, seo-mmd-2019
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>= sql-server-2017'
ms.openlocfilehash: 6f5b449b587cab543a14c9c815eac60889112ff8
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97484265"
---
# <a name="find-the-product-key-for-sql-server-reporting-services"></a>SQL Server Reporting Services의 제품 키를 찾습니다.

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2017-and-later](../../includes/ssrs-appliesto-2017-and-later.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

프로덕션 환경에 서버를 설치할 수 있도록 SSRS(SQL Server Reporting Services) 2017 및 2019의 제품 키를 찾는 방법을 알아봅니다.

제품 키를 찾으려면 먼저 SQL Server 설치 프로그램을 다운로드하고 실행합니다.

1. [SQL Server를 다운로드](../../database-engine/install-windows/install-sql-server.md)합니다.
1. SQL Server 설치 프로그램을 실행하고 미리 채워진 키를 복사합니다.

    ![SQL Server 제품 키 복사](media/find-reporting-services-product-key-ssrs/ssrs-ss2017-copy-product-key.png)

1. [Reporting Services를 다운로드](install-reporting-services.md)하고 설치 프로그램을 실행한 후, 다음과 같이 키를 붙여넣습니다.

     ![제품 키 붙여넣기](media/find-reporting-services-product-key-ssrs/ssrs-ssrs2017-paste-product-key.png)

Reporting Services를 처음 설치할 때만 이 단계를 수행해야 합니다. 서비스 업데이트에는 키를 입력할 필요가 없습니다.

## <a name="next-steps"></a>다음 단계

- [SQL Server Reporting Services 설치](install-reporting-services.md)
- 추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](https://go.microsoft.com/fwlink/?LinkId=620231)
