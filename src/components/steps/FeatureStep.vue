<template>
<!-- eslint-disable vue/no-mutating-props -->
    <div class="row justify-content-center mt-4">
        <div class="col-12 col-lg-10 col-xl-8">
            <div class="tab-content py-6 ffcpSteps">
                <div class="tab-pane fade show active">
                    <div class="row justify-content-center">
                        <div class="col-12 col-md-10 col-lg-8 col-xl-6 text-center">
                        <h3 class="mb-3">
                            Features
                        </h3>
                        <p class="mb-5 text-muted">
                            random text
                        </p>
                        </div>
                    </div>
                    <div class="form-group">
                        <div class="mb-3">
                            <label for="exampleFormControlInput1" class="form-label">Auction Data 3</label>
                            <input type="text" class="form-control" id="exampleFormControlInput1" placeholder="Some text" v-model="auction.data_txt_3">
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
    name: 'feature-step',
    props: ['auction']
}
</script>