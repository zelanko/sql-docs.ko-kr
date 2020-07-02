---
title: 데이터 정렬 및 CLR 통합 데이터 형식 | Microsoft Docs
description: SQL Server CLR 통합에서 .NET Framework 문자열 Api는 현재 스레드의 CultureInfo의 CompareInfo 속성을 사용 하 여 문자열 비교를 수행 합니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- data types [CLR integration]
- parameter collation [CLR integration]
- collations [CLR integration]
ms.assetid: 6ebaed8e-2e2b-4f6d-bf4b-bc25452de441
author: rothja
ms.author: jroth
ms.openlocfilehash: e5333da328c36ed184b3e8acbbbd8671bc0b4971
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85765344"
---
# <a name="collation-and-clr-integration-data-types"></a>데이터 정렬 및 CLR 통합 데이터 형식
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]에서는 **CompareInfo** 개체가 데이터 정렬을 처리합니다. [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 문자열 API(애플리케이션 프로그래밍 인터페이스)는 현재 스레드의 **CompareInfo** 개체와 연결된 **CultureInfo** 속성을 사용하여 문자열 비교를 수행합니다. **CultureInfo** 개체의 기본 설정은 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 로캘 설정에 기반을 둡니다. **CultureInfo** 값을 비교할 때 **System.String** 가 명시적으로 지정되지 않은 경우 이 설정에 따라 기본 비교 의미 체계가 달라집니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 **Compareinfo** 속성을 데이터베이스 또는 서버 데이터 정렬로 명시적으로 변경 하지 않습니다. 필요한 경우 사용자가 자신의 루틴에서 적절한 **CompareInfo** 속성을 설정해야 합니다.  
  
## <a name="parameter-collation"></a>매개 변수 데이터 정렬  
 CLR (공용 언어 런타임) 루틴을 만들 때 루틴에 바인딩된 CLR 메서드의 매개 변수가 **SQLString**형식이 면는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 호출 루틴을 포함 하는 데이터베이스의 기본 데이터 정렬로 매개 변수 인스턴스를 만듭니다. 매개 변수가 **SqlType** 이 아닌 경우(예: **String** 이 아닌 **SQLString**) 매개 변수에 데이터베이스의 데이터 정렬 정보가 연결되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [.NET Framework의 SQL Server 데이터 형식](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
