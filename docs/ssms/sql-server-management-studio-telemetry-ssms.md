---
title: SQL Server Management Studio - 원격 분석(SSMS) | Microsoft 문서
ms.custom: ''
ms.date: 02/20/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: c28ffa44-7b8b-4efa-b755-c7a3b1c11ce4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: abe3642cf4d74b67fcb595548a498fb062d5cddd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47633351"
---
# <a name="local-audit-for-ssms-usage-feedback-collection"></a>SSMS 사용 현황 피드백 수집에 대한 로컬 감사
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
SSMS(SQL Server Management Studio)에는 익명 기능 사용 현황 데이터를 수집하고 Microsoft에 보낼 수 있는 인터넷 사용 기능이 포함됩니다. SSMS는 표준 컴퓨터 정보 및 Microsoft로 전송되어 SSMS의 품질, 보안 및 안정성 개선의 목적으로 분석될 수 있는 사용 및 성능에 대한 정보를 수집할 수 있습니다. 사용자 이름, 주소 또는 기타 개인 정보는 수집하지 않습니다. 자세한 내용은 [SQL Server 개인정보처리방침](http://go.microsoft.com/fwlink/?LinkID=868444)을 참조하세요.

## <a name="audit-feature-usage-data"></a>기능 사용 현황 데이터 감사

SSMS를 통해 수집된 기능 사용 현황 데이터를 확인하려면 다음을 수행합니다.
1.  SSMS를 시작합니다.
2.  **보기**를 클릭하고 기본 메뉴에서 **출력**을 클릭하여 **출력** 창을 표시합니다. 
3.  **출력** 창이 표시되면 **출력 보기 선택:** 메뉴에서 **원격 분석**을 선택합니다.

SSMS를 통해 데이터베이스와 상호 작용할 경우 **출력** 창에 수집된 데이터가 표시됩니다.

## <a name="enable-or-disable-usage-feedback-collection-in-ssms"></a>SSMS에서 사용 현황 피드백 수집 사용 또는 사용 안 함

SSMS에 대한 사용 현황 데이터 수집을 포함하거나 제외하려면 [How to configure SQL Server 2016 to send feedback to Microsoft](http://support.microsoft.com/help/3153756/how-to-configure-sql-server-2016-to-send-feedback-to-microsoft)(Microsoft로 피드백을 보내도록 SQL Server 2016을 구성하는 방법)를 참조하세요.

## <a name="see-also"></a>관련 항목:

[SQL Server 사용 피드백 모음에 대한 로컬 감사](http://msdn.microsoft.com/library/mt743085.aspx)
