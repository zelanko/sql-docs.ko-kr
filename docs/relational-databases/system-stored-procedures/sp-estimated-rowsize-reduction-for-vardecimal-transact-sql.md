---
title: sp_estimated_rowsize_reduction_for_vardecimal (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_estimated_rowsize_reduction_for_vardecimal
- sp_estimated_rowsize_reduction_for_vardecimal_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_estimated_rowsize_reduction_for_vardecimal
- decimal data type, compressing
- numeric data type, compressing
- estimate decimal compression
- table compression [SQL Server]
ms.assetid: 0fe45983-f9f2-4c7f-938a-0fd96e1cbe8d
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 1d699e62251f8f2c750795d2389f338e9bd1bf11
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "37999625"
---
# <a name="spestimatedrowsizereductionforvardecimal-transact-sql"></a>sp_estimated_rowsize_reduction_for_vardecimal(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  VarDecimal 저장소 형식이 테이블에 설정되어 있는 경우 평균 행 크기의 감소를 추정합니다. 이 숫자를 사용하여 테이블 크기의 전체 감소를 추정합니다. 통계 샘플링을 사용하여 평균 행 크기의 감소를 계산하므로 이 값은 하나의 추정값으로만 간주해야 합니다. 드물긴 하지만 VarDecimal 저장소 형식을 설정한 후 행 크기가 증가할 수도 있습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 대신 ROW 및 PAGE 압축을 사용하십시오. 자세한 내용은 [Data Compression](../../relational-databases/data-compression/data-compression.md)을 참조하세요. 테이블 및 인덱스의 크기에 압축 효과 참조 하세요 [sp_estimate_data_compression_savings &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md)합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_estimated_rowsize_reduction_for_vardecimal [ [ @table_name = ] 'table'] [;]  
```  
  
## <a name="arguments"></a>인수  
 [  **@table=** ] **'***테이블***'**  
 저장소 형식을 변경할 테이블의 세 부분으로 구성된 이름입니다. *테이블* 됩니다 **nvarchar(776)** 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 현재 테이블 크기 및 예상 테이블 크기 정보를 제공하는 다음 결과 집합이 반환됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**avg_rowlen_fixed_format**|**10 진수 (12, 2)**|고정 Decimal 저장소 형식으로 행의 길이를 나타냅니다.|  
|**avg_rowlen_vardecimal_format**|**10 진수 (12, 2)**|VarDecimal 저장소 형식이 사용되는 경우 평균 행 크기를 나타냅니다.|  
|**row_count**|**int**|테이블의 행 수입니다.|  
  
## <a name="remarks"></a>Remarks  
 사용 하 여 **sp_estimated_rowsize_reduction_for_vardecimal** 테이블에 vardecimal 저장소 형식 사용 하는 경우 발생 하는 비용 절감을 예측 합니다. 예를 들어 평균 행 크기가 40% 줄어드는 경우 테이블 크기를 40% 줄일 수 있습니다. 채우기 비율과 행 크기에 따라 공간이 절약되지 않을 수도 있습니다. 예를 들어 8000바이트 길이의 행이 있고 행 크기를 40% 줄인 경우에도 여전히 데이터 페이지 하나에 행 하나만 넣을 수 있어 공간이 절약되지 않을 수 있습니다.  
  
 하는 경우의 결과 **sp_estimated_rowsize_reduction_for_vardecimal** 테이블이 확장 됨, 즉 테이블의 많은 행 사용할 작은 그리고 decimal 데이터 형식의 전체 자릿수를 거의 하 vardecimal 저장소 형식에 필요한 오버 헤드는 vardecimal 저장소 형식에서 공간 절약 보다 큽니다. 드물긴 하지만 이런 경우에는 VarDecimal 저장소 형식을 설정하지 마십시오.  
  
 사용 하 여 테이블을 vardecimal 저장소 형식을 사용 하는 경우 **sp_estimated_rowsize_reduction_for_vardecimal** vardecimal 저장소 형식을 비활성화 된 경우 행의 평균 크기를 예측 합니다.  
  
## <a name="permissions"></a>사용 권한  
 테이블에 대한 CONTROL 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Production.WorkOrderRouting` 데이터베이스의 `AdventureWorks2012` 테이블이 압축된 경우의 행 크기 감소를 추정합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_estimated_rowsize_reduction_for_vardecimal 'Production.WorkOrderRouting' ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [sp_db_vardecimal_storage_format &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-db-vardecimal-storage-format-transact-sql.md)   
 [sp_tableoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md)  
  
  
