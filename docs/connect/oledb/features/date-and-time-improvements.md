---
title: 날짜 및 시간 기능 향상 | Microsoft Docs
description: SQL Server 용 OLE DB 드라이버에서 날짜 및 시간 개선
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: c7da4795d3485f5165ac7844f00d5a46f0a29cc9
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51603673"
---
# <a name="date-and-time-improvements"></a>날짜 및 시간 기능 향상
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  이 항목에서는 OLE DB 드라이버에 추가 된 날짜 및 시간 데이터 형식에 대 한 SQL Server 지원에 대 한 설명 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]합니다.  
  
 날짜/시간 기능 향상에 대 한 자세한 내용은 참조 하세요. [날짜 및 시간 기능 향상 &#40;OLE DB&#41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)합니다.  
  
 이 기능을 보여 주는 예제 응용 프로그램에 대한 자세한 내용은 [SQL Server 데이터 프로그래밍 예제](https://msftdpprodsamples.codeplex.com/)를 참조하십시오.  
  
## <a name="usage"></a>사용법  
 다음 섹션에서는 새 date 및 time 형식을 사용하는 다양한 방법에 대해 설명합니다.  
  
### <a name="use-date-as-a-distinct-data-type"></a>고유 데이터 형식으로 Date 사용  
 부터는 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], 날짜/시간 형식에 대 한 향상 된 지원을 통해 DBTYPE_DBDATE OLE DB 형식을 사용 하는 것이 효율적입니다.  
  
### <a name="use-time-as-a-distinct-data-type"></a>고유 데이터 형식으로 Time 사용  
 OLE DB에는 정밀도가 1초인 시간(DBTYPE_DBTIME)만 포함하는 데이터 형식이 이미 있습니다.
  
 새 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] time 데이터 형식은 100나노초까지 정확한 소수 자릿수 초를 사용합니다. SQL Server 용 OLE DB 드라이버에서 새 형식을 그러려면: DBTYPE_DBTIME2 합니다. 소수 자릿수 초가 없는 시간을 사용하도록 작성된 기존 응용 프로그램은 time(0) 열을 사용할 수 있습니다. 응용 프로그램에서 메타데이터로 반환된 형식을 사용하지 않는 한 기존 OLE DB DBTYPE_TIME 형식과 해당 구조체는 올바로 작동해야 합니다.  
  
### <a name="use-time-as-a-distinct-data-type-with-extended-fractional-seconds-precision"></a>확장된 초 소수 부분 자릿수의 고유 데이터 형식으로 Time 사용  
 프로세스 제어 및 제조 응용 프로그램과 같은 일부 응용 프로그램에는 정밀도가 최대 100나노초인 시간 데이터를 처리하는 기능이 필요합니다. 새 OLE DB의이 목적을 위해 형식은 DBTYPE_DBTIME2입니다.  
  
### <a name="use-datetime-with-extended-fractional-seconds-precision"></a>확장된 초 소수 부분 자릿수의 Datetime 사용  
 OLE DB에는 정밀도가 최대 1나노초인 형식이 이미 정의되어 있습니다. 그러나 이 형식은 기존 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 응용 프로그램에서 이미 사용되고 있고 이러한 응용 프로그램에서는 1/300초의 정밀도만 허용합니다. 새 **datetime2(3)** 형식은 기존 datetime 형식과 직접 호환되지 않습니다. 이 형식이 응용 프로그램의 동작에 영향을 미칠 수 있는 경우 응용 프로그램에서 새 DBCOLUMN 플래그를 사용하여 실제 서버 유형을 확인해야 합니다.    
  
### <a name="use-datetime-with-extended-fractional-seconds-precision-and-timezone"></a>확장된 초 소수 부분 자릿수 및 표준 시간대의 Datetime 사용  
 일부 응용 프로그램에는 표준 시간대 정보가 포함된 datetime 값이 필요합니다. 이 작업은 새 DBTYPE_DBTIMESTAMPOFFSET 형식에서 지원 됩니다.
  
### <a name="use-datetimedatetimedatetimeoffset-data-with-client-side-conversions-consistent-with-existing-conversions"></a>기존 변환과 일관된 클라이언트 쪽 변환이 포함된 Date/Time/Datetime/Datetimeoffset 데이터 사용  
 변환은 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]에 도입된 모든 date 및 time 형식 간 변환을 포함하도록 일관된 방식으로 확장되었습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 기능용 OLE DB 드라이버](../../oledb/features/oledb-driver-for-sql-server-features.md)  
  
  
