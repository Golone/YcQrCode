YcQrCode
========

��ɹ��/������ά�룬�ײ� ,ģ��������Դ

�ֽżܣ�

//�������Զ�ά�����
Yc.QrcodeLib.XXX
//����QrEncode ��
QrEncode.cs
//�̳� CustomEncode
public class QrEncode : Yc.QrCodeLib.custom.CustomEncode
//������֤ 
public QrEncode(string key)
     : base(key)
 {

 }
 public override void SetParam()
 {
        base.SetParam();
        //TODO:���þ������
  }
        //���Զ�ά��������С��Ԫ
        public override Bitmap Encode(string content)
        {
            try
            {
                matrix = QrCodeEncoder.calQrcode(EnCoding.GetBytes(content));
            }
            catch { throw new Exception("���ݳ�����Χ����ѡ����߰汾���߽����ݴ���"); }

            this.SetParam();

            //SolidBrush Backbrush = new SolidBrush(QrCodeEncoder.QRCodeBackgroundColor);
            SolidBrush Backbrush = new SolidBrush(Color.Transparent);//����͸��
            SolidBrush Forebrush = new SolidBrush(QrCodeEncoder.QRCodeForegroundColor);

            Bitmap image = new Bitmap(this.QrCodeW, this.QrCodeH);
            Graphics g = Graphics.FromImage(image);

            Rectangle rect = new Rectangle();

            g.FillRectangle(Backbrush, new Rectangle(0, 0, image.Width, image.Height));

            for (int i = 0; i < matrix.Length; i++)
            {
                for (int j = 0; j < matrix.Length; j++)
                {
                    rect = new Rectangle((j + this.SpacingW) * QrCodeEncoder.QRCodeScale, (i + this.SpacingH) * QrCodeEncoder.QRCodeScale, QrCodeEncoder.QRCodeScale, QrCodeEncoder.QRCodeScale);
                    if (matrix[j][i])
                    {
                        ChangeFillShape(g, Forebrush, rect, EN_FillShape.FillRectangle, new FillShape(), Backbrush);
                    }
                    else
                        ChangeFillShape(g, Backbrush, rect, EN_FillShape.FillRectangle, new FillShape(), Backbrush);
                }
            }
            return image;
        }