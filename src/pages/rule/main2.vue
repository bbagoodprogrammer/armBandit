<template>
  <div class="rule">
    <h5>Thời gian</h5>
    <p>Thời gian: 18h 22/8~21h 1/9</p>
    <ol>
      <li>Trong thời gian sự kiện mỗi 1 xu nạp được nhận 1 bạc. Bạc dùng để quay thưởng ở giao diện sự kiện, quay càng nhiều phần thưởng càng khủng, tỷ lệ trúng phần thưởng giá trị càng cao!</li>
      <li>Mỗi lần quay thưởng có thể nhận đồng thời 3 phần thưởng gửi ngay vào tài khoản, nếu trong đó bao gồm Thẻ Nhân Đôi, 2 phần thưởng khác đều được nhận gấp đôi!</li>
      <li>Phiếu quà nạp và phiếu quà tặng nhận được trong sự kiện này bắt đầu tính từ khi quay trúng thưởng trong 24h, đủ điều kiện sẽ phát xu! Chỉ tính xu tặng trong phòng Kara, phòng radio và tác phẩm.</li>
      <li>Quý tộc được gửi trong vòng 7 ngày sau khi kết thúc sự kiện. </li>
      <li>Quay 500 Bạc/lần đủ 20 lần chắc chắn trúng ID đẹp 8 số, nếu trúng mời liên hệ ID 10 và chọn ID trong kho số của ban tổ chức.</li>
    </ol>
    <p class="waordsMsg">Phần thưởng có thể nhận</p>
    <div class="wardsBox clearfix">
      <ul>
        <li>
          <span>
            <img :src="require('../../assets/img/ward18.png')" alt="">
          </span>
          <p>Quý tộc</p>
        </li>
        <li>
          <span>
            <img :src="require('../../assets/img/ward19.png')" alt="">
          </span>
          <p>Vip</p>
        </li>
        <li>
          <span>
            <img :src="require('../../assets/img/ward12.png')" alt="">
          </span>
          <p>Vô số xu</p>
        </li>
        <li>
          <span>
            <img :src="require('../../assets/img/ward4.png')" alt="">
          </span>
          <p>Phiếu quà Nạp</p>
        </li>
        <li>
          <span>
            <img :src="require('../../assets/img/ward7.png')" alt="">
          </span>
          <p>Phiếu quà Tặng </p>
        </li>
        <li>
          <span>
            <img :src="require('../../assets/img/ward8.png')" alt="">
          </span>
          <p>Bạc</p>
        </li>
        <li>
          <span>
            <img :src="require('../../assets/img/ward21.png')" alt="">
          </span>
          <p>Thẻ Nhân Đôi</p>
        </li>
        <li>
          <span>
            <img :src="require('../../assets/img/ward15.png')" alt="">
          </span>
          <p>Vô số đậu</p>
        </li>
        <li>
          <span>
            <img :src="require('../../assets/img/ward20.png')" alt="">
          </span>
          <p>ID đẹp 8 số</p>
        </li>
      </ul>
    </div>
    <p class="footerMsg">Quyết định của ban tổ chức là quyết định cuối cùng </p>
  </div>
</template>

<script>
export default {

}
</script>

<style lang="scss">
body {
  background-color: #2b0057;
}
.rule {
  padding: 0.35rem 0.45rem;
  h5 {
    color: #fdfdac;
    font-size: 160%;
    font-weight: bold;
    text-align: center;
    margin-bottom: 0.36rem;
  }
  > p {
    font-size: 80%;
    color: #5dffe2;
  }
  ol {
    li {
      margin-top: 0.2rem;
      padding-left: 0.38rem;
      font-size: 80%;
      line-height: 0.28rem;
      position: relative;
    }
    li::after {
      content: "";
      width: 0.12rem;
      height: 0.12rem;
      position: absolute;
      left: 0rem;
      top: 0.1rem;
      background-color: #ffd900;
      border-radius: 50%;
    }
  }
  .waordsMsg {
    margin-top: 1rem;
  }
  .wardsBox {
    width: 5.5rem;
    margin: 0 auto;
    li {
      width: 1.52rem;
      float: left;
      margin: 0.2rem 0.3rem 0 0;
      span {
        display: block;
        width: 0.9rem;
        height: 0.9rem;
        border-radius: 0.2rem;
        background-color: #ab02de;
        text-align: center;
        margin: 0 auto;
        img {
          display: inline-block;
          width: 100%;
          height: 100%;
        }
      }
      p {
        font-size: 80%;
        text-align: center;
        white-space: nowrap;
        margin-top: 0.12rem;
      }
    }
  }
  .footerMsg {
    text-align: center;
    font-size: 80%;
    color: #f7d8ff;
    margin-top: 0.6rem;
  }
  .clearfix:after {
    content: "";
    height: 0;
    line-height: 0;
    display: block;
    visibility: hidden;
    clear: both;
  }
}
@import "../../assets/scss/common.scss";
</style>
