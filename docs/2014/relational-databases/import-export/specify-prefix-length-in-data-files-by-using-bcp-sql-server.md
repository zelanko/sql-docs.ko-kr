---
title: bcp를 사용하여 데이터 파일에 접두사 길이 지정(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bcp utility [SQL Server], prefix length
- prefix length [SQL Server]
- lengths [SQL Server], prefix characters
- data formats [SQL Server], prefix length
ms.assetid: ce32dd1a-26f1-4f61-b9fa-3f1feea9992e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ff16491ed9c021424d3d6371ccb7ba2941c61129
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050406"
---
# <a name="specify-prefix-length-in-data-files-by-using-bcp-sql-server"></a>bcp를 사용하여 데이터 파일에 접두사 길이 지정(SQL Server)
  원시 형식의 데이터를 데이터 파일에 대량으로 내보내는 작업에서 파일 스토리지를 가장 적게 사용하도록 하기 위해 **bcp** 명령은 각 필드의 이름 앞에 필드 길이를 나타내는 문자를 하나 이상 추가합니다. 이러한 문자를 *길이 접두사 문자*라고 합니다.  
  
## <a name="the-bcp-prompt-for-prefix-length"></a>bcp 프롬프트에서 접두사 길이 지정  
 대화형 **bcp** 명령에 **in** 또는 **out** 옵션이 포함된 경우 서식 파일 스위치( **-f**) 또는 데이터 형식 스위치( **-n**, **-c**, **-w**또는 **-N**)가 없으면 명령에서 다음과 같이 각 데이터 필드의 접두사 길이를 지정하라는 메시지가 표시됩니다.  
  
 `Enter prefix length of field <field_name> [<default>]:`  
  
 0을 지정하면 **bcp** 는 필드의 길이(문자 데이터 형식인 경우)나 필드 종결자(문자가 아닌 원시 형식인 경우)를 지정하라는 메시지를 표시합니다.  
  
> [!NOTE]  
>  **bcp** 명령의 모든 필드를 대화형으로 지정하면 명령에서 비 XML 서식 파일의 각 필드에 대한 응답을 저장하라는 메시지를 표시합니다. 비 XML 서식 파일에 대한 자세한 내용은 [비 XML 서식 파일&#40;SQL Server&#41;](xml-format-files-sql-server.md)을 참조하세요.  
  
## <a name="overview-of-prefix-length"></a>접두사 길이 개요  
 필드의 접두사 길이를 저장하려면 필드의 최대 길이를 나타낼 수 있도록 충분한 바이트가 필요합니다. 또한 필요한 바이트의 수는 파일 스토리지 유형, 열의 Null 허용 여부 및 데이터 파일에 저장된 데이터가 네이티브 형식인지 문자 형식인지 여부에 따라 달라집니다. 예를 들어 `text` 또는 `image` 데이터 형식은 4개의 접두사 문자가 필요한 반면 `varchar` 데이터 형식은 2개의 접두사 문자로 필드의 길이를 저장할 수 있습니다. 데이터 파일에서 이러한 길이 접두사 문자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 내부 이진 데이터 형식으로 저장됩니다.  
  
> [!IMPORTANT]  
>  네이티브 형식을 사용할 때는 필드 종결자 대신 길이 접두사를 사용하십시오. 네이티브 형식 데이터 파일은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 내부 이진 데이터 형식에 저장되므로 종결자와 충돌할 수 있습니다.  
  
##  <a name="prefix-lengths-for-bulk-export"></a><a name="PrefixLengthsExport"></a> 대량 내보내기의 접두사 길이  
  
> [!NOTE]  
>  필드를 내보낼 때 접두사 길이 프롬프트에 제공되는 기본값은 해당 필드에 가장 효과적인 접두사 길이를 나타냅니다.  
  
 Null 값이 빈 필드로 나타납니다. 필드가 비어 있음(NULL)을 나타내기 위해 필드 접두사에 -1을 포함하므로 최소 1바이트가 필요합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블 열에서 Null 값을 허용하는 경우 해당 열은 파일 스토리지 유형에 따라 1이상의 접두사 길이가 필요합니다.  
  
 대량 내보내기한 데이터를 네이티브 데이터 형식이나 문자 형식으로 저장하는 경우 다음 표에서 설명하는 접두사 길이를 사용하십시오.  
  
|SQL Server<br /><br /> 데이터 형식|네이티브 형식<br /><br /> NOT NULL|네이티브 형식<br /><br /> NULL|문자 형식<br /><br /> NOT NULL|문자 형식<br /><br /> NULL|  
|------------------------------|--------------------------------|----------------------------|-----------------------------------|-------------------------------|  
|`char`|2|2|2|2|  
|`varchar`|2|2|2|2|  
|`nchar`|2|2|2|2|  
|`nvarchar`|2|2|2|2|  
|`text` <sup>1</sup>|4|4|4|4|  
|`ntext` <sup>1</sup>|4|4|4|4|  
|`binary`|2|2|2|2|  
|`varbinary`|2|2|2|2|  
|`image` <sup>1</sup>|4|4|4|4|  
|`datetime`|0|1|0|1|  
|`smalldatetime`|0|1|0|1|  
|`decimal`|1|1|1|1|  
|`numeric`|1|1|1|1|  
|`float`|0|1|0|1|  
|`real`|0|1|0|1|  
|`int`|0|1|0|1|  
|`bigint`|0|1|0|1|  
|`smallint`|0|1|0|1|  
|`tinyint`|0|1|0|1|  
|`money`|0|1|0|1|  
|`smallmoney`|0|1|0|1|  
|`bit`|0|1|0|1|  
|`uniqueidentifier`|1|1|0|1|  
|`timestamp`|1|1|1|1|  
|`varchar(max)`|8|8|8|8|  
|`varbinary(max)`|8|8|8|8|  
|UDT(사용자 정의 데이터 형식)|8|8|8|8|  
|XML|8|8|8|8|  
  
 <sup>1</sup> `ntext` , `text` 및 `image` 데이터 형식은 이후 버전의에서 제거 될 예정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 입니다. 향후 개발 작업에서는 이 데이터 형식을 사용하지 않도록 하고 현재 이 데이터 형식을 사용하는 애플리케이션은 수정하세요. 대신 `nvarchar(max)`, `varchar(max)` 및 `varbinary(max)`를 사용해야 합니다.  
  
##  <a name="prefix-lengths-for-bulk-import"></a><a name="PrefixLengthsImport"></a> 대량 가져오기의 접두사 길이  
 데이터를 대량 가져올 때 접두사 길이는 해당 데이터 파일이 원래 작성될 때 지정된 값입니다. **bcp** 을 사용하여 데이터 파일을 만들지 않은 경우에는 길이 접두사 문자가 없을 수도 있습니다. 이 경우에는 접두사 길이에 0을 지정합니다.  
  
> [!NOTE]  
>  **bcp**를 사용하여 만들지 않은 데이터 파일에 접두사 길이를 지정하려면 이 항목의 앞부분에 나오는 [대량 내보내기의 접두사 길이](#PrefixLengthsExport)에 제공되어 있는 길이를 사용하세요.  
  
## <a name="see-also"></a>참고 항목  
 [bcp 유틸리티](../../tools/bcp-utility.md)   
 [데이터 형식&#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [bcp를 사용하여 필드 길이 지정&#40;SQL Server&#41;](specify-field-length-by-using-bcp-sql-server.md)   
 [필드 및 행 종결자 지정&#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)   
 [bcp를 사용하여 파일 스토리지 유형 지정&#40;SQL Server&#41;](specify-file-storage-type-by-using-bcp-sql-server.md)  
  
  
