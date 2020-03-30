---
title: SQL Server 2019 Reporting Services에서 사용되지 않는 기능 | Microsoft Docs
description: 이 문서에서는 다음 버전의 SQL Server Reporting Services에서 더 이상 사용되지 않는 기능을 설명합니다.
ms.date: 11/21/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, backward compatibility
- deprecated features [Reporting Services]
- HTML OWC rendering extension [Reporting Services]
- Report Server Web service, endpoints
ms.assetid: 3876c01e-f81d-4cce-9104-5106a8c369e6
author: maggiesMSFT
ms.author: maggies
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: eaa7edebe99a7c444fe1bfa23971317517399ea2
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "74320277"
---
# <a name="deprecated-features-in-sql-server-2019-reporting-services"></a>SQL Server 2019 Reporting Services에서 사용되지 않는 기능

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2019-and-later](../includes/ssrs-appliesto-2019-and-later.md)] [!INCLUDE [ssrs-appliesto-pbirs](../includes/ssrs-appliesto-pbirs.md)]

특정 기능이 사용되지 않는 기능으로 표시되면 이는 곧 다음을 의미합니다.

- 기능이 유지 관리 모드로만 유지됩니다. 새 기능과의 상호 운용성과 관련된 변경 작업을 포함하여 새로운 변경 작업을 수행하지 않습니다.
- 업그레이드를 더욱 용이하게 할 수 있도록 사용되지 않는 기능을 되도록이면 향후 릴리스에서 제거하지 않으려고 합니다. 드문 경우지만 이로 인해 향후 혁신에 제한이 있다면 Reporting Services에서 해당 기능이 영구적으로 제거될 수도 있습니다.
- 새로운 개발 작업에서는 사용되지 않는 기능을 사용하지 않는 것이 좋습니다.

**향후 버전의 SQL Server에서 사용되지 않는 기능**

SQL Server Reporting Services는 다음 버전의 SQL Server에서 다음 기능을 지원하지만 이후 버전에서 사용 중단됩니다. 어떤 버전의 SQL Server에서 제거될지는 결정되지 않았습니다.

| **범주** | **사용되지 않는 기능** | **대체 기능** |
| --- | --- | --- |
| 보고서 서버 | 보고서 파트 갤러리 | None |
| 보고서 서버 | 모바일 보고서 및 모바일 보고서 게시자 | Power BI Report Server에서 Power BI 보고서는 모바일 기능을 제공합니다. |
| 보고서 서버 | XLS 및 DOC 렌더링 형식 | .XLSX 및 DOCX 형식이 사용 가능하고 지원됩니다. |
| 보고서 서버 | Atom 데이터 피드 | oData 피드는 SSRS 및 Power BI Report Server의 공유 데이터 세트에 대해 지원됩니다. |

## <a name="see-also"></a>참고 항목

[SQL Server 2019 Reporting Services(SSRS)에서 지원되지 않는 기능](discontinued-functionality-sql-server-reporting-services-2019.md)

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](https://go.microsoft.com/fwlink/?LinkId=620231)
