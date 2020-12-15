---
description: SQL Server Native Client 날짜 및 시간 기능 향상
title: 날짜 및 시간 기능 향상 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.reviewer: ''
ms.prod: sql
ms.technology: native-client
ms.topic: reference
ms.assetid: 9b1d0d9d-1f6e-4399-8f61-e23f9a486a7a
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c7b5a802c430ce958e448edeac3066cd0012021f
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97463394"
---
# <a name="sql-server-native-client-date-and-time-improvements"></a>SQL Server Native Client 날짜 및 시간 기능 향상
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  이 항목에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에 추가된 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]Native Client의 date 및 time 데이터 형식 지원에 대해 설명합니다.  
  
 날짜/시간 기능 향상에 대 한 자세한 내용은 [ODBC&#41;&#40;](../../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)OLE DB&#41;및 날짜 및 시간 향상 [&#40;날짜 및 시간 향상](../../../relational-databases/native-client-ole-db-date-time/date-and-time-improvements-ole-db.md) 을 참조 하세요.  
  
 이 기능을 보여 주는 예제 애플리케이션에 대한 자세한 내용은 [SQL Server 데이터 프로그래밍 예제](https://msftdpprodsamples.codeplex.com/)를 참조하십시오.  
  
## <a name="usage"></a>사용  
 다음 섹션에서는 새 date 및 time 형식을 사용하는 다양한 방법에 대해 설명합니다.  
  
### <a name="use-date-as-a-distinct-data-type"></a>고유 데이터 형식으로 Date 사용  
 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]부터는 date/time 형식에 대한 향상된 지원을 통해 SQL_TYPE_DATE ODBC 형식(ODBC 2.0 애플리케이션의 경우 SQL_DATE) 및 DBTYPE_DBDATE OLE DB 형식을 보다 효율적으로 사용할 수 있습니다.  
  
### <a name="use-time-as-a-distinct-data-type"></a>고유 데이터 형식으로 Time 사용  
 OLE DB에는 정밀도가 1초인 시간(DBTYPE_DBTIME)만 포함하는 데이터 형식이 이미 있습니다. ODBC에서 이에 해당하는 형식은 SQL_TYPE_TIME(ODBC 2.0 애플리케이션의 경우 SQL_TIME)입니다.  
  
 새 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] time 데이터 형식은 100나노초까지 정확한 소수 자릿수 초를 사용합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client에서 이 형식을 사용하려면 새 DBTYPE_DBTIME2(OLE DB) 및 SQL_SS_TIME2(ODBC) 형식이 필요합니다. 소수 자릿수 초가 없는 시간을 사용하도록 작성된 기존 애플리케이션은 time(0) 열을 사용할 수 있습니다. 애플리케이션에서 메타데이터로 반환된 형식을 사용하지 않는 한 기존 OLE DB DBTYPE_TIME 및 ODBC SQL_TYPE_TIME 형식과 해당 구조체는 올바로 작동해야 합니다.  
  
### <a name="use-time-as-a-distinct-data-type-with-extended-fractional-seconds-precision"></a>확장된 초 소수 부분 자릿수의 고유 데이터 형식으로 Time 사용  
 프로세스 제어 및 제조 애플리케이션과 같은 일부 애플리케이션에는 정밀도가 최대 100나노초인 시간 데이터를 처리하는 기능이 필요합니다. 이를 위해 새 DBTYPE_DBTIME2(OLE DB) 및 SQL_SS_TIME2(ODBC) 형식이 추가되었습니다.  
  
### <a name="use-datetime-with-extended-fractional-seconds-precision"></a>확장된 초 소수 부분 자릿수의 Datetime 사용  
 OLE DB에는 정밀도가 최대 1나노초인 형식이 이미 정의되어 있습니다. 그러나 이 형식은 기존 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 애플리케이션에서 이미 사용되고 있고 이러한 애플리케이션에서는 1/300초의 정밀도만 허용합니다. 새 **datetime2(3)** 형식은 기존 datetime 형식과 직접 호환되지 않습니다. 이 형식이 애플리케이션의 동작에 영향을 미칠 수 있는 경우 애플리케이션에서 새 DBCOLUMN 플래그를 사용하여 실제 서버 유형을 확인해야 합니다.  
  
 ODBC에도 정밀도가 최대 1나노초인 형식이 이미 정의되어 있습니다. 그러나 이 형식은 기존 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 애플리케이션에서 이미 사용되고 있고 이러한 애플리케이션에서는 3밀리초의 정밀도만 허용합니다. 새 **datetime2 (3)** 형식은 기존 **datetime** 형식과 직접 호환 되지 않습니다. **datetime2(3)** 의 정밀도는 1밀리초이고 **datetime** 의 정밀도는 1/300초입니다. ODBC 애플리케이션에서는 설명자 필드 SQL_DESC_TYPE_NAME으로 사용 중인 서버 유형을 확인할 수 있습니다. 따라서 기존 SQL_TYPE_TIMESTAMP(ODBC 2.0 애플리케이션의 경우 SQL_TIMESTAMP) 형식을 두 형식 모두에 사용할 수 있습니다.  
  
### <a name="use-datetime-with-extended-fractional-seconds-precision-and-timezone"></a>확장된 초 소수 부분 자릿수 및 표준 시간대의 Datetime 사용  
 일부 애플리케이션에는 표준 시간대 정보가 포함된 datetime 값이 필요합니다. 이러한 값은 새 DBTYPE_DBTIMESTAMPOFFSET(OLE DB) 및 SQL_SS_TIMESTAMPOFFSET(ODBC) 형식을 통해 지원됩니다.  
  
### <a name="use-datetimedatetimedatetimeoffset-data-with-client-side-conversions-consistent-with-existing-conversions"></a>기존 변환과 일관된 클라이언트 쪽 변환이 포함된 Date/Time/Datetime/Datetimeoffset 데이터 사용  
 ODBC 표준은 기존 date, time 및 timestamp 형식 간 변환이 작동하는 방법에 대해 설명합니다. 이러한 변환은 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]에 도입된 모든 date 및 time 형식 간 변환을 포함하도록 일관된 방식으로 확장되었습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client 기능](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
