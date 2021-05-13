<template>
	<div class="banner">
		<img class="w-100" src="https://png.pngtree.com/thumb_back/fh260/back_our/20190621/ourmid/pngtree-quartz-watch-promotion-season-atmospheric-black-banner-image_184423.jpg">
		<div class="banner-overlay d-flex align-items-center">
			<div class="banner-text w-50 text-left">
				<h4 class="banner-title font-weight-bolder">DIGITAL NOON Store</h4>
				<p class="card-text">DIGITAL NOON Store – Cửa hàng bán đồng hồ Thụy Sỹ cao cấp chính hãng số 1 Hà Nội – Giá chiết khấu từ 20-40% cho tất cả các sản phẩm – Dịch vụ của chúng tôi bảo hành quốc tế theo tiêu chuẩn hãng – Order nhanh chóng.</p>
				<button class="btn btn-outline-primary px-4">Mua ngay</button>
			</div>
			<div class="w-50"></div>
		</div>
	</div>
</template>

<script>
export default {
	name: "Banner",
};
</script>

<style scoped>
h4 {
	color: #eacc82;
}
p {
	color: white;
}
.banner {
	position: relative;
}

.banner-overlay {
	background-color: rgba(0, 0, 0, 0.377);
	position: absolute;
	top: 0;
	left: 0;
	right: 0;
	bottom: 0;
}
.banner-text {
	padding: 0 180px 0 180px;
}

.banner-text > .btn {
	color: #eacc82;
	border-color: #eacc82;
}
.banner-text > .btn:hover {
	color: white;
	background-color: #eacc82;
}
</style>