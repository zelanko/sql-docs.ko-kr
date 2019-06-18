---
title: SSRS(SQL Server 2017 Reporting Services)의 제품 키 찾기 | Microsoft Docs
ms.date: 12/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 36460943b233f02e4d029b7865c7d7fa3844b488
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65502919"
---
# <a name="how-to-find-the-product-key-for-sql-server-2017-reporting-services"></a>SQL Server 2017 Reporting Services의 제품 키를 찾는 방법

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2017-and-later](../../includes/ssrs-appliesto-2017-and-later.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

프로덕션 환경에 서버를 설치할 수 있도록 SSRS(SQL Server 2017 Reporting Services)의 제품 키를 찾는 방법을 알아봅니다.

제품 키를 찾으려면 먼저 SQL Server 2017 설치 프로그램을 다운로드하고 실행합니다.

1. 다음 원본 중 하나에서 SQL Server 2017을 다운로드합니다.

    - 볼륨 라이선스 서비스 센터
    - MSDN 구독
    - 소매(Microsoft Store에서 다운로드)

1. SQL Server 2017 설치 프로그램을 실행하고 미리 채워진 키를 복사합니다.

    ![SQL Server 2017 제품 키 복사](media/find-reporting-services-product-key-ssrs/ssrs-ss2017-copy-product-key.png)

1. [Reporting Services 설치 프로그램을 실행](install-reporting-services.md)하고 키를 붙여넣습니다.

     ![제품 키 붙여넣기](media/find-reporting-services-product-key-ssrs/ssrs-ssrs2017-paste-product-key.png)

SSRS 2017을 처음 설치할 때만 이 단계를 수행해야 합니다. 서비스 업데이트에는 키를 입력할 필요가 없습니다.

## <a name="related-information"></a>관련 정보

- SQL Server Reporting Services 기본 모드를 설치하는 방법에 대한 자세한 내용은 [Reporting Services 기본 모드 보고서 서버 설치](install-reporting-services-native-mode-report-server.md)를 참조하세요. 

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

- SharePoint 통합 모드에서 SQL Server 2016 Reporting Services 이하 버전을 설치하는 방법에 대한 자세한 내용은 [SharePoint 모드에서 첫 번째 보고서 서버 설치](install-the-first-report-server-in-sharepoint-mode.md)를 참조하세요.

::: moniker-end

## <a name="next-steps"></a>다음 단계

- [SQL Server 2017 Reporting Services 설치](install-reporting-services.md)
- 추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](https://go.microsoft.com/fwlink/?LinkId=620231)
