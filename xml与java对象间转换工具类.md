# Xml与java对象相互转换

```
import java.io.StringReader;
import java.io.StringWriter;

import javax.xml.bind.JAXBContext;
import javax.xml.bind.JAXBException;
import javax.xml.bind.Marshaller;
import javax.xml.bind.Unmarshaller;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

/**
 * <xml与java对象相互转化>
 * <功能详细描述>
 * 
 * @author  daijunmin
 * @version  [版本号, 2018年8月29日]
 * @see  [相关类/方法]
 * @since  [产品/模块版本]
 */
public class XmlAndJavaObjectConvert
{
    private static final Logger logger = LoggerFactory.getLogger(XmlAndJavaObjectConvert.class);
    
    /**
     * <java对象转换为xml>
     * <功能详细描述>
     * @author  daijunmin
     * 创建时间:  2018年8月29日
     * @param obj
     * @return
     * @see [类、类#方法、类#成员]
     */
    public static String convertToXml(Object obj)
    {
        // 创建输出流  
        StringWriter sw = new StringWriter();
        try
        {
            // 利用jdk中自带的转换类实现  
            JAXBContext context = JAXBContext.newInstance(obj.getClass());
            Marshaller marshaller = context.createMarshaller();
            // 格式化xml输出的格式  
            marshaller.setProperty(Marshaller.JAXB_FORMATTED_OUTPUT, Boolean.TRUE);
            // 将对象转换成输出流形式的xml  
            marshaller.marshal(obj, sw);
        }
        catch (JAXBException e)
        {
            logger.info("XmlAndJavaObjectConvert java convertTo Xml err={}", e);
        }
        return sw.toString();
    }
    
    /**
     * <xml转换为指定的java对象>
     * <功能详细描述>
     * @author  daijunmin
     * 创建时间:  2018年8月29日
     * @param clazz
     * @param xmlStr
     * @return
     * @see [类、类#方法、类#成员]
     */
    public static Object convertXmlStrToObject(Class clazz, String xmlStr)
    {
        Object xmlObject = null;
        try
        {
            JAXBContext context = JAXBContext.newInstance(clazz);
            // 进行将Xml转成对象的核心接口  
            Unmarshaller unmarshaller = context.createUnmarshaller();
            StringReader sr = new StringReader(xmlStr);
            xmlObject = unmarshaller.unmarshal(sr);
        }
        catch (JAXBException e)
        {
            logger.info("XmlAndJavaObjectConvert Xml convertTo java err={}", e);
        }
        return xmlObject;
    }
}

```