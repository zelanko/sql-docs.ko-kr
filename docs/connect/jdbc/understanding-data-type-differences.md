---
title: 이해 데이터 형식 차이 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ab8fa00f-cb16-47e2-94b8-3a76f56c2b84
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ad1294145856f99b9ed99fb89ead3c35a8478080
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="understanding-data-type-differences"></a>데이터 형식 차이 이해
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Java 프로그래밍 언어 데이터 형식 간의 차이점 중 여러 가지 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 데이터 형식입니다. [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 다양 한 형식 변환 기능을 통해 이러한 차이 손쉽게 극복 합니다.  
  
## <a name="character-types"></a>문자 형식  
 JDBC 문자열 데이터 형식은 **CHAR**, **VARCHAR**, 및 **LONGVARCHAR**합니다. JDBC 드라이버는 JDBC 4.0 API를 지원합니다. JDBC 4.0에서는 JDBC 문자열 데이터 형식이 될 수도 있습니다 **NCHAR**, **NVARCHAR**, 및 **LONGNVARCHAR**합니다. 이러한 새 문자열 형식은 유니코드 형식으로 Java 네이티브 문자 형식을 유지하므로 ANSI와 Unicode 간 변환을 수행할 필요가 없습니다.  
  
|형식|Description|  
|----------|-----------------|  
|고정 길이|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **char** 및 **nchar** 데이터 형식은 JDBC에 직접 매핑됩니다 **CHAR** 및 **NCHAR** 형식입니다. 이는 해당 열에 SET ANSI_PADDING ON이 설정된 경우 서버에서 패딩을 제공하는 고정 길이 형식입니다. 패딩이 항상 설정 되어 대 한 **nchar**, 하지만 **char**, 서버 char 열이 패딩 되지 않은 경우에서 JDBC 드라이버는에서 패딩을 추가 합니다.|  
|가변 길이|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **varchar** 및 **nvarchar** 형식은 JDBC에 직접 매핑됩니다 **VARCHAR** 및 **NVARCHAR** 각각 형식입니다.|  
|Long|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **텍스트** 및 **ntext** 형식은 JDBC에 매핑됩니다 **LONGVARCHAR** 및 **LONGNVARCHAR** 각각 입력 합니다. 이러한 형식은 사용 되지 않는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)]큰 값 형식을 사용 해야 하므로 **varchar (max)** 또는 **nvarchar (max)**, 대신 합니다.<br /><br /> 업데이트를 사용 하 여\<숫자 유형 > 및 [updateObject (int, java.lang.Object)](../../connect/jdbc/reference/updateobject-method-int-java-lang-object.md) 에 대 한 메서드가 실패 합니다 **텍스트** 및 **ntext** 서버 열입니다. 그러나 사용 하는 [setObject](../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md) 에 대해 지정 된 문자 변환 형식과 함께 메서드는 지원 **텍스트** 및 **ntext** 서버 열입니다.|  
  
## <a name="binary-string-types"></a>이진 문자열 형식  
 JDBC 이진 문자열 형식은 **이진**, **VARBINARY**, 및 **LONGVARBINARY**합니다.  
  
|형식|Description|  
|----------|-----------------|  
|고정 길이|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **이진** JDBC에 직접 매핑됩니다 **이진** 유형입니다. 이는 해당 열에 SET ANSI_PADDING ON이 설정된 경우 서버에서 패딩을 제공하는 고정 길이 형식입니다. 서버 char 열이 패딩되지 않으면 JDBC 드라이버가 패딩을 추가합니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **타임 스탬프** 형식은 JDBC **이진** 고정 길이가 8 바이트의 형식입니다.|  
|가변 길이|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **varbinary** JDBC에 매핑됩니다 **VARBINARY** 유형입니다.<br /><br /> **udt** 에 입력 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] JDBC로 매핑되는 **VARBINARY** 유형입니다.|  
|Long|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **이미지** JDBC에 매핑됩니다 **LONGVARBINARY** 유형입니다. 이 형식은 부터는 사용 되지 [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)]큰 값 형식인을 사용 해야 하므로 **varbinary (max)** 대신 합니다.|  
  
## <a name="exact-numeric-types"></a>정확한 숫자 형식  
 JDBC의 정확한 숫자 형식은 해당되는 SQL Server 형식에 바로 매핑됩니다.  
  
|형식|Description|  
|----------|-----------------|  
|BIT|JDBC **비트** 형식은 단일 비트 0 또는 1 일 수를 나타냅니다. 매핑되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **비트** 유형입니다.|  
|TINYINT|JDBC **TINYINT** 형식은 1 바이트를 나타냅니다. 매핑되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **tinyint** 유형입니다.|  
|SMALLINT|JDBC **SMALLINT** 형식은 부호 있는 16 비트 정수를 나타냅니다. 매핑되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **smallint** 유형입니다.|  
|INTEGER|JDBC **정수** 형식은 부호 있는 32 비트 정수를 나타냅니다. 매핑되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **int** 유형입니다.|  
|bigint|JDBC **BIGINT** 형식은 부호 있는 64 비트 정수를 나타냅니다. 매핑되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **bigint** 유형입니다.|  
|NUMERIC|JDBC **숫자** 형식은 동일한 전체 자릿수 값을 포함 하는 고정 전체 자릿수 소수 값을 나타냅니다. **숫자** 형식에 매핑됩니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **숫자** 유형입니다.|  
|DECIMAL|JDBC **10 진수** 형식은 지정 된 전체 자릿수 값을 하나 이상 포함 하는 고정 전체 자릿수 10 진수 값을 나타냅니다. **10 진수** 형식에 매핑됩니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **10 진수** 유형입니다.<br /><br /> JDBC **10 진수** 형식에도 매핑됩니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **money** 및 **smallmoney** 8과 4에 저장 되어 있는 특정 고정 전체 자릿수 소수 형식은 형식 바이트, 각각.|  
  
## <a name="approximate-numeric-types"></a>근사 숫자 형식  
 JDBC 근사 숫자 형식은 **실제**, **DOUBLE**, 및 **FLOAT**합니다.  
  
|형식|Description|  
|----------|-----------------|  
|REAL|JDBC **실제** 유형 자릿수는 7 (단 정밀도) 전체 자릿수 및 변수에 직접 매핑되고는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **실제** 유형입니다.|  
|DOUBLE|JDBC **DOUBLE** 유형 15 (배정밀도) 전체 자릿수는 및에 매핑됩니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **float** 유형입니다. JDBC **FLOAT** 의 동의어 **DOUBLE**합니다. 혼동 될 수 있으므로 **FLOAT** 및 **DOUBLE**, **DOUBLE** 는 것이 좋습니다.|  
  
## <a name="datetime-types"></a>날짜 및 시간 형식  
 JDBC **타임 스탬프** 형식에 매핑됩니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **datetime** 및 **smalldatetime** 형식입니다. **datetime** 형식은 4 바이트 정수 두 개에 저장 됩니다. **smalldatetime** 형식 동일한 정보 (날짜 및 시간)을 보유 하지만 덜 정확도, 2 바이트 small 정수와에서 합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **타임 스탬프** 형식은 고정 길이 이진 문자열 형식입니다. JDBC 시간 형식에 매핑되지 않는: **날짜**, **시간**, 또는 **타임 스탬프**합니다.  
  
## <a name="custom-type-mapping"></a>사용자 지정 형식 매핑  
 사용자 지정 형식 매핑 기능은 JDBC에 대 한 sql 데이터 인터페이스를 사용 하는 jdbc 고급 형식 (Udt, Struct, 및 등). JDBC 드라이버에 구현되어 있지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [JDBC 드라이버 데이터 형식 이해](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
