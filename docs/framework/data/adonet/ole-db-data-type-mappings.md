---
title: OLE DB 데이터 형식 매핑
ms.date: 03/30/2017
ms.assetid: 04bcb259-59d3-4fd7-894d-4f0dd0c68069
ms.openlocfilehash: 7f3b498e39feac4a6fe98e739793d20e0268b8f4
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91150702"
---
# <a name="ole-db-data-type-mappings"></a>OLE DB 데이터 형식 매핑

다음 표에서는 ADO 및 OLE DB에 대 한 .NET Framework Data Provider의 데이터 형식에 대 한 유추 된 .NET Framework 형식 ()을 보여 줍니다 <xref:System.Data.OleDb> . 또한 이 표에는 <xref:System.Data.OleDb.OleDbDataReader>의 형식화된 접근자 메서드도 나열되어 있습니다.  
  
|ADO 형식|OLE DB 형식|.NET Framework 형식|.NET Framework 형식화 된 접근자|  
|--------------|-----------------|----------------------------------------------------------------------|--------------------------------------------------------------------------------|  
|adBigInt|DBTYPE_I8|Int64|GetInt64()|  
|adBinary|DBTYPE_BYTES|Byte[]|GetBytes()|  
|adBoolean|DBTYPE_BOOL|부울|GetBoolean()|  
|adBSTR|DBTYPE_BSTR|String|GetString()|  
|adChapter|DBTYPE_HCHAPTER|`DataReader`를 통해 지원됩니다. [DataReader를 사용 하 여 데이터 검색을](retrieving-data-using-a-datareader.md)참조 하세요.|GetValue()|  
|adChar|DBTYPE_STR|String|GetString()|  
|adCurrency|DBTYPE_CY|Decimal|GetDecimal()|  
|adDate|DBTYPE_DATE|DateTime|GetDateTime()|  
|adDBDate|DBTYPE_DBDATE|DateTime|GetDateTime()|  
|adDBTime|DBTYPE_DBTIME|DateTime|GetDateTime()|  
|adDBTimeStamp|DBTYPE_DBTIMESTAMP|DateTime|GetDateTime()|  
|adDecimal|DBTYPE_DECIMAL|Decimal|GetDecimal()|  
|adDouble|DBTYPE_R8|Double|GetDouble()|  
|adError|DBTYPE_ERROR|ExternalException|GetValue()|  
|adFileTime|DBTYPE_FILETIME|DateTime|GetDateTime()|  
|adGUID|DBTYPE_GUID|GUID|GetGuid()|  
|adIDispatch|DBTYPE_IDISPATCH *|Object|GetValue()|  
|adInteger|DBTYPE_I4|Int32|GetInt32()|  
|adIUnknown|DBTYPE_IUNKNOWN *|Object|GetValue()|  
|adNumeric|DBTYPE_NUMERIC|Decimal|GetDecimal()|  
|adPropVariant|DBTYPE_PROPVARIANT|Object|GetValue()|  
|adSingle|DBTYPE_R4|Single|GetFloat()|  
|adSmallInt|DBTYPE_I2|Int16|GetInt16()|  
|adTinyInt|DBTYPE_I1|Byte|GetByte()|  
|adUnsignedBigInt|DBTYPE_UI8|UInt64|GetValue()|  
|adUnsignedInt|DBTYPE_UI4|UInt32|GetValue()|  
|adUnsignedSmallInt|DBTYPE_UI2|UInt16|GetValue()|  
|adUnsignedTinyInt|DBTYPE_UI1|Byte|GetByte()|  
|adVariant|DBTYPE_VARIANT|Object|GetValue()|  
|adWChar|DBTYPE_WSTR|String|GetString()|  
|adUserDefined|DBTYPE_UDT|지원되지 않음||  
|adVarNumeric|DBTYPE_VARNUMERIC|지원되지 않음||  
  
 \* OLE DB 형식 및의 `DBTYPE_IUNKNOWN` 경우 `DBTYPE_IDISPATCH` 개체 참조는 포인터의 마샬링된 표현입니다.  
  
## <a name="see-also"></a>참고 항목

- [ADO.NET에서 데이터 검색 및 수정](retrieving-and-modifying-data.md)
- [ADO.NET 개요](ado-net-overview.md)
