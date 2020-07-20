---
title: Allow PolyBase Export 구성 옵션 | Microsoft Docs
description: SQL Server 설정에서 `allow polybase export` 구성 옵션 설정
ms.custom: ''
ms.date: 07/10/2020
ms.prod: sql
ms.prod_service: ''
ms.reviewer: ''
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c25a7e42b55561ed6337281497e847999d722292
ms.sourcegitcommit: dacd9b6f90e6772a778a3235fb69412662572d02
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2020
ms.locfileid: "86279656"
---
# <a name="set-allow-polybase-export-configuration-option"></a>`allow polybase export` 구성 옵션 설정

[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

`allow polybase export` 서버 구성 옵션을 사용하여 Hadoop 외부 테이블에 `INSERT`할 수 있습니다. 

이 기능은 다른 외부 데이터 원본에 대한 삽입을 지원하지 않습니다.

 다음 표에서는 이 옵션에 사용할 수 있는 값을 설명합니다. 

| 값 | 의미                                |
|-------|----------------------------------------|
| 0     | 사용 안 함. 이 값은 기본 설정입니다. |
| 1     | 사용                                |


설정은 즉시 적용됩니다.

## <a name="example"></a>예제

다음 예에서는 이 설정을 사용하도록 설정합니다.

```sql
sp_configure 'show advanced options', 1;
GO
RECONFIGURE;
GO
sp_configure 'allow polybase export', 0;
GO
RECONFIGURE;
GO
```

## <a name="next-steps"></a>다음 단계

 [데이터 내보내기](../../relational-databases/polybase/polybase-configure-hadoop.md#exporting-data)