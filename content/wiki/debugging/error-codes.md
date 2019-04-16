---
id: 392
title: Error Codes
date: 2010-12-17T10:38:15+00:00
description: Common error codes, causes and solutions.
parent: debugging
---

## HRESULT

https://msdn.microsoft.com/en-us/library/cc231198.aspx

The HRESULT numbering space is vendor-extensible. Vendors can supply their own values for this field, as long as the C bit (0x20000000) is set, indicating it is a customer code.

The HRESULT numbering space has the following internal structure. Any protocol that uses NTSTATUS values on the wire is responsible for stating the order in which the bytes are placed on the wire.

* S (1 bit): Severity. If set, indicates a failure result. If clear, indicates a success result.
* R (1 bit): Reserved. If the N bit is clear, this bit MUST be set to 0. If the N bit is set, this bit is defined by the NTSTATUS numbering space (as specified in section 2.3).
* C (1 bit): Customer. This bit specifies if the value is customer-defined or Microsoft-defined. The bit is set for customer-defined values and clear for Microsoft-defined values.<1>
* N (1 bit): If set, indicates that the error code is an NTSTATUS value (as specified in section 2.3), except that this bit is set.
* X (1 bit):  Reserved.  SHOULD be set to 0. <2>
* Facility (11 bits): An indicator of the source of the error. New facilities are occasionally added by Microsoft.
* Code (16 bits)


<table border="0" cellspacing="2" cellpadding="2" width="891">
  <tr>
    <td valign="top" width="163">
      Error Id
    </td>
    
    <td valign="top" width="121">
      Error Text
    </td>
    
    <td valign="top" width="121">
      HRESULT (hex)
    </td>
    
    <td valign="top" width="121">
      HRESULT (dec)
    </td>
    
    <td valign="top" width="118">
      Description
    </td>
    
    <td valign="top" width="131">
      Solutions
    </td>
    
    <td valign="top" width="98">
      More Info
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="172">
      E_FAIL
    </td>
    
    <td valign="top" width="120">
      Unspecified error
    </td>
    
    <td valign="top" width="120">
      0x80004005
    </td>
    
    <td valign="top" width="120">
      -2147467259
    </td>
    
    <td valign="top" width="117">
      &nbsp;
    </td>
    
    <td valign="top" width="132">
      &nbsp;
    </td>
    
    <td valign="top" width="97">
      &nbsp;
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="176">
      REGDB_E_CLASSNOTREG
    </td>
    
    <td valign="top" width="119">
      Class not registered
    </td>
    
    <td valign="top" width="118">
      0x80040154
    </td>
    
    <td valign="top" width="119">
      &nbsp;
    </td>
    
    <td valign="top" width="115">
      Class not registered
    </td>
    
    <td valign="top" width="131">
      The COM library is not registered. Find what DLL defines the class ID in the rest of the error message, and register it.
    </td>
    
    <td valign="top" width="94">
      &nbsp;
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="186">
      &nbsp;
    </td>
    
    <td valign="top" width="118">
      &nbsp;
    </td>
    
    <td valign="top" width="118">
      800700c1
    </td>
    
    <td valign="top" width="118">
      &nbsp;
    </td>
    
    <td valign="top" width="114">
      &nbsp;
    </td>
    
    <td valign="top" width="131">
      Mixing 32/64 problem? Compile to x86 instead of All Platforms for .NET assembly
    </td>
    
    <td valign="top" width="93">
      &nbsp;
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="190">
      E_OUTOFMEMORY
    </td>
    
    <td valign="top" width="118">
      &nbsp;
    </td>
    
    <td valign="top" width="117">
      8007000e
    </td>
    
    <td valign="top" width="118">
      &nbsp;
    </td>
    
    <td valign="top" width="114">
      &nbsp;
    </td>
    
    <td valign="top" width="130">
      &nbsp;
    </td>
    
    <td valign="top" width="92">
      &nbsp;
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="192">
      TYPE_E_CANTLOADLIBRARY
    </td>
    
    <td valign="top" width="116">
      &nbsp;
    </td>
    
    <td valign="top" width="115">
      80029c4a
    </td>
    
    <td valign="top" width="116">
      &nbsp;
    </td>
    
    <td valign="top" width="112">
      The type library or DLL could not be loaded
    </td>
    
    <td valign="top" width="129">
      Type library not found, or maybe missing dependency loaded using LoadLibrary?
    </td>
    
    <td valign="top" width="89">
      &nbsp;
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="205">
      &nbsp;
    </td>
    
    <td valign="top" width="115">
      &nbsp;
    </td>
    
    <td valign="top" width="115">
      800a005e
    </td>
    
    <td valign="top" width="115">
      &nbsp;
    </td>
    
    <td valign="top" width="111">
      Invalid use of Null
    </td>
    
    <td valign="top" width="129">
      Probably coming from a VB6 COM DLL, where a Null value is being used improperly (i.e., something is Null that shouldn't be)
    </td>
    
    <td valign="top" width="87">
      &nbsp;
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="209">
      &nbsp;
    </td>
    
    <td valign="top" width="115">
      &nbsp;
    </td>
    
    <td valign="top" width="115">
      80070005
    </td>
    
    <td valign="top" width="115">
      &nbsp;
    </td>
    
    <td valign="top" width="111">
      &nbsp;
    </td>
    
    <td valign="top" width="128">
      Permissions problem when registering DLL? Make sure you are in an elevated command prompt when trying to register (Administrator in the command window)
    </td>
    
    <td valign="top" width="87">
      &nbsp;
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="211">
      TYPE_E_REGISTRYACCESS
    </td>
    
    <td valign="top" width="115">
      &nbsp;
    </td>
    
    <td valign="top" width="115">
      8002801c
    </td>
    
    <td valign="top" width="115">
      &nbsp;
    </td>
    
    <td valign="top" width="111">
      Error accessing the OLE registry
    </td>
    
    <td valign="top" width="128">
      &nbsp;
    </td>
    
    <td valign="top" width="87">
      &nbsp;
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="211">
      &nbsp;
    </td>
    
    <td valign="top" width="115">
      &nbsp;
    </td>
    
    <td valign="top" width="115">
      900a005e
    </td>
    
    <td valign="top" width="116">
      &nbsp;
    </td>
    
    <td valign="top" width="112">
      &nbsp;
    </td>
    
    <td valign="top" width="129">
      A VB6 result error code (more info needed)
    </td>
    
    <td valign="top" width="90">
      &nbsp;
    </td>
  </tr>
</table>

When searching for the decimal code, be aware most search engines will exclude that term from search results because of the negative sign. Instead, surround the term with speech marks to prevent that: "-2147467259"   
Try various searches for the hex code, decimal code and constant to find various results   
Sometimes the error code will be from another platform or framework, for example, 900a005e is from VB6.

## Example

REGDB\_E\_CLASSNOTREG

The error code will look like this in .NET: 0x80040154 (word) or 0xFFFFFFFF80040154 (dword), or a decimal value of 2147746132 (1 word) or –2147221164 (dword)

Here's how it looks defined in winerror.h:

#define REGDB\_E\_CLASSNOTREG \_HRESULT\_TYPEDEF_(0x80040154L)

## References

[Online version of winerror.h @ msdn.microsoft.com](http://msdn.microsoft.com/en-us/library/ms819772.aspx) &#8211; Contains a bunch of error codes, from which you can get the constant name, and possibly some more information