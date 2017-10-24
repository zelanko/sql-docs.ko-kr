---
title: SET TEXTSIZE (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 04/12/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- TEXTSIZE_TSQL
- TEXTSIZE
- SET_TEXTSIZE_TSQL
- SET TEXTSIZE
dev_langs:
- TSQL
helpviewer_keywords:
- SET TEXTSIZE statement
- SELECT statement [SQL Server], text size returned
- size [SQL Server], text and image data
- TEXTSIZE option
- text size returned [SQL Server]
ms.assetid: 787154a6-39a6-4dd6-a6d0-67b4364f95d5
caps.latest.revision: 38
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2d9925b382a7d09722846ca7da583fb92fe4609c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="set-textsize-transact-sql"></a>SET TEXTSIZE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  크기를 지정 **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, **텍스트**, **ntext** 및 **이미지** SELECT 문에 의해 반환 된 데이터입니다.  
  
> [!IMPORTANT]  
>  **ntext**, **텍스트**, 및 **이미지** 데이터 형식은 나중 버전의에서 제거 됩니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. 향후 개발 작업에서는 이 데이터 형식을 사용하지 않도록 하고 현재 이 데이터 형식을 사용하는 응용 프로그램은 수정하세요. 대신 **nvarchar(max)**, **varchar(max)**및 **varbinary(max)** 를 사용합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
SET TEXTSIZE { number }   
```  
  
## <a name="arguments"></a>인수  
 *number*  
 길이가 **varchar (max)**, **nvarchar (max)**, **varbinary (max)**, **텍스트**, **ntext**, 또는 **이미지** 데이터 (바이트)입니다. *번호* 는 정수 이며 최대값은 2147483647 (2GB)입니다.  값이-1은 무제한 크기를 나타냅니다. 값이 0 기본값인 4KB으로 크기를 다시 설정합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 10.0 이상 및 ODBC Driver for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 자동으로 지정 `-1` (무제한) 경우에 연결 합니다.  
  
 **다음 보다 오래 된 드라이버 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008:** 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 드라이버 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 (버전 9)에 대 한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 연결 될 때 TEXTSIZE를 2147483647 자동으로 설정 합니다.  
  
## <a name="remarks"></a>주의  
 SET TEXTSIZE 영향을 줌 설정의 @@TEXTSIZE 함수입니다.  
  
 SET TEXTSIZE 옵션은 실행 시간 또는 런타임에 설정되며, 구문 분석 시에는 설정되지 않습니다.  
  
## <a name="permissions"></a>Permissions  
 **public** 역할의 멤버 자격이 필요합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [@@TEXTSIZE&#40;Transact-SQL&#41;](../../t-sql/functions/textsize-transact-sql.md)   
 [데이터 형식&#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  

