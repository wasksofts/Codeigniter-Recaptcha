# Codeigniter-Recaptcha
Google v2 Codeigniter Recaptcha

# Controller
    $this->form_validation->set_rules('g-recaptcha-response', 'Checkbox', 'trim|xss_clean|required|callback__check_recaptcha');
  
    $this->data['show_captcha'] = TRUE;
                if ($this->data['use_recaptcha'] == 1) {
                    $this->data['recaptcha_html'] = $this->_create_recaptcha();
                }
                
                /**
     * Callback function. Check if reCAPTCHA test is passed.
     *
     * @access  public
     * @return	bool
     */
    public function _check_recaptcha()
    {
        $this->load->library('recaptcha', [
            'public_key' => $this->authen->setting->recaptcha_public_key,
            'private_key' => $this->authen->setting->recaptcha_private_key
        ]);

        // Check if the form is submitted
        $resp = $this->recaptcha->is_valid();

        if (!$resp['success']) {
            $this->form_validation->set_message('_check_recaptcha', 'Check captcha checkbox');
            return FALSE;
        }
        return TRUE;
    }

    /**
     * Create reCAPTCHA JS and non-JS HTML to verify user as a human
     *
     * @access  public 
     * @return	string
     */
    public function _create_recaptcha()
    {
        $this->load->library('recaptcha', [
            'public_key' => $this->authen->setting->recaptcha_public_key,
            'private_key' => $this->authen->setting->recaptcha_private_key
        ]);

        $html = $this->recaptcha->create_box();

        return  $html;
    }
                
# view
 
           <?php if ($show_captcha) {
                if ($use_recaptcha == 1) { ?>
                    <script src='https://www.google.com/recaptcha/api.js'></script>
                    <div class="row">
                        <div class="col-md-12">
                            <?php echo $recaptcha_html; ?>
                        </div>
                    </div>
            <?php }
            } ?>
 
 
