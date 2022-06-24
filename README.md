Hi softmatterlab,
moving from deeptrack 2.0 to 2.1 the generation of a sphere image with the command 

````python
def generate_simulated_image(
    image_size=(64, 64), pix_size=5.2, z_pix_size = 0.1,
    radius=(7.06/2) * 1e-6, ri=1.59, z=2541, apod_val=0.3, 
    sigma = 0.025, add_noise=False,
):
    sphere_main = dt.Sphere(
        position=(32, 32),
        position_unit="pixel",
        cam_pix_size=pix_size,
        radius=radius,
        refractive_index=ri,
        z=z / z_pix_size,
    )

    optics = dt.Brightfield(
        wavelength=633e-9,
        NA=1,
        resolution=[pix_size * 1e-6, pix_size * 1e-6, z_pix_size * 1e-6],
        magnification=1,
        refractive_index_medium=1.33,
        upscale=1,
        padding = 1*[1,1,1,1],
        pupil = dt.GaussianApodization(sigma=apod_val),
        output_region=(0, 0, image_size[0], image_size[1]),
    )

    noise = dt.Gaussian(mu=0, sigma=sigma)

    sphere_main_no = lambda: np.random.randint(1, 2)

    sample_normal = sphere_main ^ sphere_main_no

    if add_noise:
        image_formed = optics(sample_normal) >> noise
    else:
        image_formed = optics(sample_normal)

    image = image_formed.update().resolve()

    return np.array(image[:,:,0])
````