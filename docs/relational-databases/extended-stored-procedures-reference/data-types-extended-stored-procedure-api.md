---
title: 데이터 형식(확장 저장 프로시저 API) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], data types
- data types [SQL Server], extended stored procedures
ms.assetid: 37fb86b9-8819-4387-bcdc-9616968e15ad
author: rothja
ms.author: jroth
ms.openlocfilehash: 1e135e6706454fe1f03b4c7ab762e5234e1b7d35
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68064210"
---
# <a name="data-types-extended-stored-procedure-api"></a>데이터 형식(확장 저장 프로시저 API)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]대신 CLR 통합을 사용 하세요.  
  
 확장 저장 프로시저 API 데이터 형식을 사용하려면 프로그램에 Srv.h 헤더 파일을 포함합니다.  
  
|데이터 형식|SQL Server 데이터 형식|Description|  
|---------------|--------------------------|-----------------|  
|SRVBIGBINARY|**binary**|**binary** 데이터 형식, 길이가 0 ~ 8000 바이트입니다.|  
|SRVBIGCHAR|**char**|**문자** 데이터 형식이 며 길이는 0 ~ 8000 바이트입니다.|  
|SRVBIGVARBINARY|**varbinary**|길이가 0-8000바이트인 가변 길이 **binary** 데이터 형식입니다.|  
|SRVBIGVARCHAR|**varchar**|길이가 0-8000바이트인 가변 길이 **character** 데이터 형식입니다.|  
|SRVBINARY|**binary**|**binary** 데이터 형식입니다.|  
|SRVBIT|**조금**|**bit** 데이터 형식입니다.|  
|SRVBITN|**비트 null**|**bit** 데이터 형식, null 값이 허용 됩니다.|  
|SRVCHAR|**char**|**문자** 데이터 형식입니다.|  
|SRVDATETIME|**datetime**|8바이트 **datetime** 데이터 형식입니다.|  
|SRVDATETIM4|**smalldatetime**|4바이트 **smalldatetime** 데이터 형식입니다.|  
|SRVDATETIMN|**datetime null**|**smalldatetime** 또는 **datetime** 데이터 형식으로 null 값이 허용 됩니다.|  
|SRVDECIMAL|**진수가**|**decimal** 데이터 형식입니다.|  
|SRVDECIMALN|**decimal null**|**decimal** 데이터 형식으로 null 값이 허용 됩니다.|  
|SRVFLT4|**실제로**|4바이트 **real** 데이터 형식입니다.|  
|SRVFLT8|**float**|8바이트 **float** 데이터 형식입니다.|  
|SRVFLTN|**실수** &#124; **float null**|**real** 또는 **float** 데이터 형식으로 null 값이 허용 됩니다.|  
|SRVIMAGE|**image**|**image** 데이터 형식입니다.|  
|SRVINT1|**tinyint**|1바이트 **tinyint** 데이터 형식입니다.|  
|SRVINT2|**smallint**|2바이트 **smallint** 데이터 형식입니다.|  
|SRVINT4|**int**|4바이트 **int** 데이터 형식입니다.|  
|SRVINTN|**tinyint** &#124; **smallint** &#124; **int null**|**tinyint**, **smallint**또는 **int** 데이터 형식으로 null 값이 허용 됩니다.|  
|SRVMONEY4|**smallmoney**|4바이트 **smallmoney** 데이터 형식입니다.|  
|SRVMONEY|**money**|8바이트 **money** 데이터 형식입니다.|  
|SRVMONEYN|**money** &#124; **smallmoney null**|**smallmoney** 또는 **money** 데이터 형식으로 null 값이 허용 됩니다.|  
|SRVNCHAR|**nchar**|유니코드 **character** 데이터 형식입니다.|  
|SRVNTEXT|**ntext**|유니코드 **text** 데이터 형식입니다.|  
|SRVNUMERIC|**번호**|**numeric** 데이터 형식입니다.|  
|SRVNUMERICN|**숫자 null**|**numeric** 데이터 형식, null 값이 허용 됩니다.|  
|SRVNVARCHAR|**nvarchar**|유니코드 가변 길이 **character** 데이터 형식입니다.|  
|SRVTEXT|**text**|**text** 데이터 형식입니다.|  
|SRVVARBINARY|**varbinary**|가변 길이 **binary** 데이터 형식입니다.|  
|SRVVARCHAR|**varchar**|가변 길이 **character** 데이터 형식입니다.|  
  
> [!IMPORTANT]  
>  확장 저장 프로시저의 원본 코드를 철저히 검토하고 프로덕션 서버에 DLL을 설치하기 전에 컴파일한 DLL을 테스트해야 합니다. 보안 검토 및 테스트에 대한 자세한 내용은 [Microsoft 웹 사이트](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/)를 참조하십시오.  
  
  
