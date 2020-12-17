---
title: SQL Server 2017 Reporting Services에서 사용되지 않는 기능 | Microsoft Docs
description: 이 문서에서는 다음 버전의 SQL Server Reporting Services에서 더 이상 사용되지 않는 기능을 설명합니다.
ms.date: 11/20/2019
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
monikerRange: '>= sql-server-2017'
ms.openlocfilehash: 553432d2e79069da19eacdd193be9b3b3e7d498c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97425318"
---
# <a name="deprecated-features-in-sql-server-2017-reporting-services"></a>SQL Server 2017 Reporting Services에서 사용되지 않는 기능

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2017](../includes/ssrs-appliesto-2017.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../includes/ssrs-appliesto-not-pbirs.md)]

특정 기능이 사용되지 않는 기능으로 표시되면 이는 곧 다음을 의미합니다.

- 기능이 유지 관리 모드로만 유지됩니다. 새 기능과의 상호 운용성과 관련된 변경 작업을 포함하여 새로운 변경 작업을 수행하지 않습니다.
- 업그레이드를 더욱 용이하게 할 수 있도록 사용되지 않는 기능을 되도록이면 향후 릴리스에서 제거하지 않으려고 합니다. 드문 경우지만 이로 인해 향후 혁신에 제한이 있다면 Reporting Services에서 해당 기능이 영구적으로 제거될 수도 있습니다.
- 새로운 개발 작업에서는 사용되지 않는 기능을 사용하지 않는 것이 좋습니다.

## <a name="features-deprecated-in-the-next-version-of-sql-server"></a>다음 버전의 SQL Server에서 사용되지 않는 기능

다음 SQL Server 2017 Reporting Services 기능은 다음 버전의 SQL Server에서는 사용되지 않습니다. 새 개발 작업에서는 이러한 기능을 사용하지 말고, 현재 이러한 기능을 사용하는 애플리케이션은 가능한 한 빨리 수정하세요.

> [!NOTE]
> 이 목록은 SQL Server 2016 Reporting Services(13.x) 목록과 동일합니다. SQL Server 2017 Reporting Services(14.x)에 대해 발표된 새로운 기능이나 지원되지 않는 기능은 없습니다.


| **범주** | **사용되지 않는 기능** | **대체 기능** |
| --- | --- | --- |
| 보고서 서버 | HTML 4.0 Renderer. | HTML 5 renderer |

## <a name="see-also"></a>참고 항목

[SSRS(SQL Server Reporting Services)에서 지원되지 않는 기능](discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)

추가 질문이 있으신가요? [Reporting Services 포럼에서 질문하기](https://go.microsoft.com/fwlink/?LinkId=620231)
