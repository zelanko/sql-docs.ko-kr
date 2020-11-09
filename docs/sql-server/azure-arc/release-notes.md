---
title: Azure Arc 지원 SQL Server - 릴리스 정보
description: 최신 릴리스 정보
author: anosov1960
ms.author: sashan
ms.reviewer: mikeray
ms.date: 10/29/2020
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 3dcbc6b17d5abe87aabe923d70746d65595b9de6
ms.sourcegitcommit: dc3ea1696b8a4332934568439aed6cce4e9737eb
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/03/2020
ms.locfileid: "93244655"
---
# <a name="release-notes---azure-arc-enabled-sql-server-preview"></a>릴리스 정보 - Azure Arc 지원 SQL Server(미리 보기)

> [!NOTE]
> 미리 보기 기능으로, 이 문서에 제시된 기술에는 [Microsoft Azure 미리 보기에 대한 보충 사용 약관](https://azure.microsoft.com/support/legal/preview-supplemental-terms/)이 적용됩니다.

## <a name="september-2020"></a>2020년 9월

Azure Arc 지원 SQL Server는 퍼블릭 미리 보기로 릴리스되었습니다. Azure Arc 지원 SQL Server는 고객 데이터 센터, 에지 또는 다중 클라우드 환경에서 Azure 외부에 호스트된 SQL Server 인스턴스로 Azure 서비스를 확장합니다.

자세한 내용은 [Azure Arc 지원 SQL Server 개요](overview.md)를 참조하세요.

### <a name="known-issues"></a>알려진 문제

다음 문제는 9월 릴리스에 적용됩니다.

* **Azure Arc 지원 SQL Server 등록** 블레이드는 사용자 지정 태그 구성을 지원하지 않습니다. 사용자 지정 태그를 추가하려면 등록 후 **SQL Server - Azure Arc** 리소스를 열고 **개요** 페이지에서 태그를 변경합니다.

* Azure Arc에 SQL Server 인스턴스를 연결하려면 광범위 권한 세트를 포함하는 계정이 필요합니다. 자세한 내용은 [필요한 권한](overview.md#required-permissions)을 참조하세요.

## <a name="october-2020"></a>2020년 10월

10월 업데이트는 다음 향상된 기능을 포함합니다.

* 이제 Azure Arc 지원 SQL Server 등록 블레이드에는 **태그** 탭이 포함됩니다. 태그는 등록 스크립트에 포함되고 **SQL Server - Azure Arc** 리소스에 반영됩니다. 자세한 내용은 [Azure Arc에 SQL Server 연결](connect.md)을 참조하세요.

* 이제 **환경 상태** 항목은 *CustomScriptExtension* 배포를 통한 포털에서 **SQL 평가** 활성화를 지원합니다. 자세한 내용은 [SQL 평가 구성](assess.md#run-on-demand-sql-assessment)을 참조하세요.

### <a name="known-issues"></a>알려진 문제

다음 문제는 10월 릴리스에 적용됩니다.

* Azure Arc에 SQL Server 인스턴스를 연결하려면 광범위 권한 세트를 포함하는 계정이 필요합니다. 자세한 내용은 [필요한 권한](overview.md#required-permissions)을 참조하세요.

## <a name="next-steps"></a>다음 단계

**작업을 시도해보시겠습니까?**  [Azure Arc 지원 SQL Server 빠른 시작](https://aka.ms/AzureArcSqlServerJumpstart)으로 빠르게 시작합니다.
