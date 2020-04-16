---
title: UTF-16 지원
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: f2520424-8ef4-409f-8147-d83da5076e96
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e81de975a3f8e2d5549ee968fc7e47bb5e3746c3
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388401"
---
# <a name="utf-16-support-in-sql-server-native-client-110"></a>SQL Server Native Client 11.0의 UTF-16 지원
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]부터는 열 결과 또는 출력 매개 변수를 바인딩할 때 고정 길이 버퍼를 제공하는 경우, 종결 문자 이전에 버퍼에 작성된 **wchar** 문자가 서로게이트 쌍의 상위 서로게이트 코드 포인트인 경우 및 다음 **wchar** 문자가 하위 서로게이트 코드 포인트인 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에서 상위 서로게이트 코드 포인트를 버퍼에 추가하지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client 기능](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
